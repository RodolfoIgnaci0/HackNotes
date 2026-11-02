webdav es una funcionalidad de windows que permite agregar, eliminar y modificar contenido en sitios web en iis.

herramientas utiles:
- davtest -> hace una serie de chequeos para revisar con que formato esta permitido operar y que permiso se tiene con cada extensión
	-  davtest  -url http://192.168.100.1/webdav -auth bob:password
- cadaver -> funciona  simil a ftp, se puede subir/bajar/borrar archivo con formato permitido, obtenido con davtest. (la idea es subir una revshell)
	-  cadaver http://192.168.100.1/webdav

usando metasploit eta el modulo "windows/iis/iis_webdav_upload_asp" //usar dependiendo del tipo de archivo que tiene execute (dato obtenido con davtest)