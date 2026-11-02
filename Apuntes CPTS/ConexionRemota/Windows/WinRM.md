La Administración remota de Windows (`WinRM`) es un protocolo de administración remota integrado de Windows simple basado en la línea de comandos.
Con WinRM, es posible ejecutar un comando remoto en otro servidor.
Puerto TCP 5985 y 5986

#### Footprinting
```
nmap -sV -sC 10.129.201.248 -p5985,5986 --disable-arp-ping -n
```

#### Interacción

##### Windows
Se puede usar powershell, con la herramienta Test-WsMan
https://learn.microsoft.com/en-us/powershell/module/microsoft.wsman.management/test-wsman?view=powershell-7.6&viewFallbackFrom=powershell-7.2
##### Linux
```
evil-winrm -i 10.129.201.248 -u Cry0l1t3 -p P455w0rD!
```
