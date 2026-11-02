
**Windows**  dentro de la shell del equipo
	hostname -> nombre del host
	systeminfo -> muestra toda la info del sistema desde la infraestructura hasta los hotfixes instalados
	wmic qfe get Caption,Description,HotFixID,InstalledOn -> muestra info de los hotfixes
	whoami /priv -> muestra privilegios de usuario
	query user -> muestra usuarios logeados
	
	net users -> muestra cuentas existentes
	net user administrator -> muestra información de la cuenta administrator
	
	net localgroup -> lista todos los grupos del sistema
	net localgroup administrators -> muestra cuentas que pertenecen al grupo administrators

**redes**
	arp -a -> descrubre otras ip en la misma red
	route print -> muestra rutas ipv4 e ipv6
	
**servicios**
	net start -> lista servicios
	wmic service list brief -> otra forma de listar servicios
	tasklist /SVC -> aplicaciones corriendo
	schtask /query /fo LIST /v -> lista de tareas programadas

 ------
 Existen modulos en msfconsole de post-explotación que brindan otro tipo de información
	 post/window/gather/enum_logged_on_users -> devuelve los usuarios que han logeado al sistema y se encuentran logeados



