####################### SMB (similar a FTP)
Listar
 smbclient -L //host_ip -N 
   -L -> listar
   -N -> no pedir contraseña

 smbmap -> permite listar volumenes y sus permisos
  smbmap -H host_ip
 
Acceder
 smbclient //host_ip/volumen -N

NOTA:- si se tienen credenciales usar --user=USERNAME --password=PASSWORDo o -U 'username%password' 
     - para cuentas de dominio usar -W

*enumeracion*
enum4linux -a target2.ine.local


-------
------
**Windows
Como smbmap, sirve para saber permisos que tiene el usuario**
```
crackmapexec smb 10.201.68.142 -u 'ybob317' -p 'ybob317' --shares
```
- Para acceder se puede seguir usando smbclient
```
smbclient //target2.ine.local/C$ -U administrator
```

- **Teniendo credenciales tambien se puede usar psexec para realizar ejecucion de comandos**

---------------------

**Conectar desde windows, con herramientas de windows**
- Desde metasploit
```
CTRL + C
migrate -N explorer.exe
shell
net view 10.0.28.125 -> listo los recursos compartidos del smb
```
- Acceso a los recursos
```
net use D: \\10.0.28.125\Documents
net use K: \\10.0.28.125\K$
```
- Luego puedo entrar, listar, copiar o hacer lo que se quiera. de igual manera puedo volver al meterpreter y estos "discos" quedan disponibles si quisiera descargar los archivos
```
dir D:
dir K:
```

![[Pasted image 20260103054131.png]]