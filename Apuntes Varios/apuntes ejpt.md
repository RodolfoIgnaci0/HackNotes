
non-staged-payload -> payload que se envia al objetivo completo con el exploit
staged-payload -> payload que se envia en dos partes, primero se establece conexión y luego se descarga la segunda parte del payload y se ejecuta
	staged -> primera parte donde se hace la conexion
	stage -> segunda parte donde se ejecuta el payload


**reconocimiento
comando: dnsrecon -d google.com
web: dnsdumpster.com
comando: wafw00f google.com #validar si se tiene waf 

google dorks: site: google.com inurl: panel filetype: pdf cache: google.com
waybackmachine -> maneja snapshot de sitios en el tiempo

scan de red: 
 - sudo nmap -sn 192.168.100.0/24 (si se scanea misma red a la conectada, usa ARP, si no, ICMP)
 - sudo nmap -sn -Pn puerto_si_ e_quiere 192.168.100.1 (manda paquete TCP a puerto especificado) (mucho mas rapido)
 - sudo netdiscover -i eth0 -r 192.168.100.0/24
 - fping -a -g 192.168.100.0/24 (poco fiable, usa ICMP)

------------

nmap desde msfconsole:
 - levantar servicio postgresql -> services start postgresql
 - generar un workspace -> workspace -a nombre
 - lanzar nmap en msfconsole -> db_nmap -sS -p- ...
 - se almacena automatico y se puede revisar con comandos "host" y "services"

importar desde archivo xml a msfconsole:
- levantar servicios postgresql
- generar un workspace
- importar data desde xml -> db_import archivo.xml
- se almacena automatico y se puede revisar con comandos "host" y "services"




-----------------
*Recomienda exploits de metasploit a usar*
load db_autopwn
db_autopwn -p -t -PI puerto -t  -> 

NOTA: solo funciona si se tiene la data de nmap importada al workspace de metasploit

otra opcion es usar analyze en metasploit, que devuelve algo mas acotado que el anterior.

-----------------
NOTA: se puede buscar a tecnologia requerida con "search type: auxiliary name: tecnologia (mysql, http, ftp,etc)"

modulos interesantes para http:
- auxiliary/scanner/http/apache_userdir_enum
- auxiliary/scanner/http/brute_dirs
- auxiliary/scanner/http/dir_scanner
- auxiliary/scanner/http/dir_listing
- auxiliary/scanner/http/http_put
- auxiliary/scanner/http/files_dir
- auxiliary/scanner/http/http_login
- auxiliary/scanner/http/http_header
- auxiliary/scanner/http/http_version
- auxiliary/scanner/http/robots_txt

modulos interesantes para mysql
- auxiliary/admin/mysql/mysql_sql -> tirar consultas  a la bd no es continua, solo reconoce contexto de la consulta actual, necesita credenciales

-------------
**Elevar privilegios y datos de metasploit**

	- Estando en meterpreter se puede usar el comando getsystem para que automaticamente corran procesos para poder elevar privilegios
	- Existe el modulo multi/recon/local_exploit_suggester, el cual dandole una sesion se encarga de evaluar el sistema y te recomienda modulos explotables para elevar privilegios

**en instalaciones masivas, credenciales utilizadas quedan en archivo C:\Windows\Panther\Unattend.xml o C:\Windows\Panther\Autounattend.xml, este queda encodiado en base64**


agregar a usuario a sudoers
```usuario ALL=NOPASSWD:ALL >> /etc/sudoers```

buscar archivos relacioandos en crontab, asociado a file specifico (busca archivos que hacen cosas con el file que es parte del crontab)
```
grep -rnw /usr -e "/home/student/message"
/usr/local/share/copy.sh: cp /home/student/message /tmp/message
```



------
limpieza de registros en meterpreter
```
clearev --> borra los registros de logs de windows
```

----
escalada de privilegios, chkrootkit tiene un exploit desde la version 0.5 hacia abajo
```
unix/local/chkrootkit
```

------

enumerar servicios corriendo, luego se puede interactuar usando nc ip puerto
```
netstat -tuln 127.0.0.1

www-data@target1:/$ netstat -tuln
netstat -tuln
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State      
tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:21              0.0.0.0:*               LISTEN     
tcp        0      0 127.0.0.1:8888          0.0.0.0:*               LISTEN     
tcp        0      0 127.0.0.11:42717        0.0.0.0:*               LISTEN     
udp        0      0 127.0.0.11:38413        0.0.0.0:*                          
www-data@target1:/$ nc 127.0.0.1 8888
```


-----

AV Evasion

- Shellter ->  requiere tener instalado Wine32 para compatibilidad en linux
	- Funciona insertando el payload en un ejecutable valido
```
	cd /usr/share/windows-resources/shellter
	sudo wine shellter.exe -> dara un wizard para proceder, preguntando donde inyectara el payload
	
	NOTA: se reemplazara el archivo que se dio con uno malicioso y se hace un backup del original en /usr/share/windows-resources/shellter/backup
```

-----
Ofuscación de código PowerShell

-  Invoke-Obfuscation -> https://github.com/danielbohannon/Invoke-Obfuscation
	- entrega un wizard para realizar distintos tipos de ofuscacion de código que se use en powershell, app necesita ser ejecutado en powershell, pero existe un packete en kali que puede correr powershell sin problemas.
