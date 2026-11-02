script diseñado para ayudar pentester a identificar potenciales subida de privilegios en windows

https://github.com/411Hall/JAWS

Se descarga el archivo raw desde el github y se ejecuta desde shell de la maquina windows (terminal del windows atacado)
```
powershell.exe -ExecutionPolicy Bypass -File .\jaws-enum.ps1 -OutputFilename JAWS-Enum.txt
```

para descargar a tu equipo la salida, se puede usar la opcion download de meterpreter
```
download JAWS-Enum.txt
```

Entrega un informe con info varia sobre el equipo
![[Pasted image 20260124220628.png]]