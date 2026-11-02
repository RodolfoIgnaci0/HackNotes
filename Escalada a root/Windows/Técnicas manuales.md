
### Permiso de SeImpersonatePrivilege
- Con el ejecutable PrintSpoofer podemos elevar privilegios a NT Authority/System

Copiamos el  ejecutable en la maquina atacada
```
scp PrintSpoofer64.exe david@target.ine.local:"C:\\Users\\david\\"
```

Ejecución
```
PrintSpoofer64.exe -i -c cmd
```
	-i -> corre el comando en modo interactivo, permitiendo interactuar con la sesión elevada
	-c cmd -> especifica el comando a ejecutar, en este caso dará un cmd.exe con privilegios elevados

------
**Elevar privilegios y datos de metasploit**

	- Estando en meterpreter se puede usar el comando getsystem para que automaticamente corran procesos para poder elevar privilegios
	- Existe el modulo multi/recon/local_exploit_suggester, el cual dandole una sesion se encarga de evaluar el sistema y te recomienda modulos explotables para elevar privilegios

**en instalaciones masivas, credenciales utilizadas quedan en archivo C:\Windows\Panther\Unattend.xml o C:\Windows\Panther\Autounattend.xml, este queda encodiado en base64**