cambiar permisos de archivos
```
icacls flag
```
![[Pasted image 20260129004211.png]]

En este caso nt authority/system tiene permisos denegados, los cuales pueden ser retitrados con:
```
icacls flag /remove:d "NT AUTHORITY\SYSTEM"
```
https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/icacls

------
