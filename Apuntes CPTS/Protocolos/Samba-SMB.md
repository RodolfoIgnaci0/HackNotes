https://academy.hackthebox.com/app/module/112/section/1067

#### Rpcclient
sirve para conexiones smb
```
rpcclient -U "" 10.129.14.128
```

| **Consulta**              | **Descripción**                                                                 |
| ------------------------- | ------------------------------------------------------------------------------- |
| `srvinfo`                 | Información del servidor.                                                       |
| `enumdomains`             | Enumere todos los dominios que se implementan en la red.                        |
| `querydominfo`            | Proporciona información de dominio, servidor y usuario de dominios desplegados. |
| `netshareenumall`         | Enumera todas las acciones disponibles.                                         |
| `netsharegetinfo <share>` | Proporciona información sobre una parte específica.                             |
| `enumdomusers`            | Enumera a todos los usuarios de dominio.                                        |
| `queryuser <RID>`         | Proporciona información sobre un usuario específico.                            |

#### Ejemplo de enumeración de usuarios
```
rpcclient $> enumdomusers

user:[mrb3n] rid:[0x3e8]
user:[cry0l1t3] rid:[0x3e9]


rpcclient $> queryuser 0x3e9

        User Name   :   cry0l1t3
        Full Name   :   cry0l1t3
        Home Drive  :   \\devsmb\cry0l1t3
        Dir Drive   :
        Profile Path:   \\devsmb\cry0l1t3\profile
        Logon Script:
        Description :
        Workstations:
        Comment     :
        Remote Dial :
        Logon Time               :      Do, 01 Jan 1970 01:00:00 CET
        Logoff Time              :      Mi, 06 Feb 2036 16:06:39 CET
        Kickoff Time             :      Mi, 06 Feb 2036 16:06:39 CET
        Password last set Time   :      Mi, 22 Sep 2021 17:50:56 CEST
        Password can change Time :      Mi, 22 Sep 2021 17:50:56 CEST
        Password must change Time:      Do, 14 Sep 30828 04:48:05 CEST
        unknown_2[0..31]...
        user_rid :      0x3e9
        group_rid:      0x201
        acb_info :      0x00000014
        fields_present: 0x00ffffff
        logon_divs:     168
        bad_password_count:     0x00000000
        logon_count:    0x00000000
        padding1[0..7]...
        logon_hrs[0..21]...
```



------
------
------
### Otras opciones
##### Enum4Linux-ng
Tambien sirve para enumerar de manera automarizada recursos de smb
```
enum4linux-ng 10.129.42.100 -A
```

-------
-------
##### Smbmap 
```
smbmap -H 10.129.42.100 
```

-------
------

##### Crackmapexec 
```
crackmapexec smb 10.129.14.128 --shares -u '' -p ''
```

-------
------
##### Impacket - Samrdump.py
```
samrdump.py 10.129.14.128
```

-----
-----
##### NetExecRM
revisar permisos del usuario para cada directorio del smb
```
netexec smb 10.129.42.197 -u "user" -p "password" --shares
```

-----
-----
##### Smbclient
```
smbclient -U user \\\\10.129.42.197\\SHARENAME
```