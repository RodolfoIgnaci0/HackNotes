comandos para obtener información

Datos Host :
	hostname -> nombre equipo
	cat /etc/issue -> distribución del equipo
	cat /etc/\*release -> datos del distribución y version
	uname -r -> version del kernel

env -> variables de entorno

Datos Hardware:
	lscpu -> datos de la cpu
	lsblk | grep sd -> información del disco
	dpkg -l  -> lista paquetes instalados en debian junto a versiones

Usuarios y grupos:
	cat /etc/passwd -> listar archivo con usuarios
	groups -> listar grupos
	groups root -> lista los grupos del usuario root
	cat /etc/group -> archivo de configuracion
	last -> lista usuarios que se han conectado
	lastlog -> lista de usuarios y si se han conectado

Redes:
	ifconfig -all -> lista ip 
	netstat -> lista de conexiones
	route -> tabla de ruteo
	cat /etc/network -> configuracion de la red, opcion si ifconfig o ip addr no funciona
	cat /etc/host -> lista de host/ip con comunicacion
	cat /etc/resolv.conf -> datos del dns que se conecta
	arp -a -> lista tabla arp en busca de otras redes // meterpreter igual cuenta con comando arp entregando info de manera mas visual

Crontab:
	ls /etc/cron* -> lista tareas programadas

------
### Semi-Automatizando enumeración con meterpreter (piden session)
linux/gather/enum_configs -> enumera archivos de configuración
linux/gather/enum_network -> enumera info de redes
linux/gather/enum_system -> enumera el sistema e info de usuario

-----
### Automatizando enumeración con linenum

Linenum, script que automatiza el proceso de toma de información desde el host
https://github.com/rebootuser/LinEnum

forma básica de ejecución: 
	./linenum.sh 