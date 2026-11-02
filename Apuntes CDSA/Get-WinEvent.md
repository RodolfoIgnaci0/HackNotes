Filtrar registros evtx mediante powershell

Filtro por id tipo 7 y que en message sea ilike dismcore, y despliego toda la información con format-list
```
Get-WinEvent -FilterHashtable @{Path='C:\Logs\DLLHijack\*.evtx'; Id=7} | Where-Object { $_.Properties[5].Value -like '*DismCore.dll*' } | Format-List
```

Para mostrar un valor especifico dentro del campo message uso el foreach-object
```
Get-WinEvent -FilterHashtable @{Path='C:\Logs\DLLHijack\*.evtx'; Id=(7,10)} | ForEach-Object { $_.Properties[5].Value }
```

Where-object sirve para filtrar
```
Get-WinEvent -FilterHashtable @{Path='C:\Logs\PowershellExec\*.evtx'; Id=10} | Where-Object { $_.Properties[8].Value -in '0x1FFFFF','0x1F3FFF','0x1F0FFF' }
```