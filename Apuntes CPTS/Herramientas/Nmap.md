uso base
```
nmap <scan types> <options> <target>
```
------

-sS -> escaneo sigiloso - no completa el 3 way handshake 
-sT -> escaneo completo sobre puertos TCP
-sU -> escaneo sobre puertos UDP
-sn -> realiza escaneo de ping
-PE -> realiza el scaneo de ping usando ICMP
--disable-arp-ping -> Desactiva el ping ARP
--packet-trace -> muestra todos los paquetes enviados y recibidos
-Pn -> deshabilita las solicitudes ICMP
-n -> deshabilita resolución DNS
--disable-arp-ping deshabilita ARP ping
-iL -> se le puede pasar listado de ips a escanear
```
nmap -sn -oA tnet -iL hosts.lst
```

-F -> scan de los 100 primeros puertos
-p- -> scan de todos los puertos
-sV -> info adicional del puerto, como versiones

-D RND:5 -> Genera cinco direcciones IP aleatorias que indican la IP de origen de la que proviene la conexión.

-------
```
nmap 10.129.2.28 -n -Pn -p 445 -O -S 10.129.2.200 -e tun0
```
-S -> Escanea el destino mediante la diferente dirección IP de origen.
-e tun0 -> Envía todas las peticiones a través de la interfaz especificada.

--source-port 53 -> Realiza los escaneos desde el puerto de origen especificado.

#### Guardado de scaneo
```
sudo nmap 10.129.2.28 -p- -oA target
```
-oN -> version nmap (mismo q salida normal)
-oG -> version grepeable
-oX -> version en xml
-oA -> guarda en las 3 versiones


con la version xml se puede realizar un reporte rapido en html
```
xsltproc target.xml -o target.html
```
### Estados de puertos

|**Estado**|**Descripción**|
|---|---|
|`open`|Esto indica que se ha establecido la conexión al puerto escaneado. Estas conexiones pueden ser **conexiones TCP**, **datagramas UDP** así como **asociaciones SCTP**.|
|`closed`|Cuando el puerto se muestra como cerrado, el protocolo TCP indica que el paquete que recibimos contiene un `RST`Bandera. Este método de escaneo también se puede utilizar para determinar si nuestro objetivo está vivo o no.|
|`filtered`|Nmap no puede identificar correctamente si el puerto escaneado está abierto o cerrado porque no se devuelve ninguna respuesta del destino para el puerto o obtenemos un código de error del destino.|
|`unfiltered`|Este estado de un puerto solo se produce durante la exploración **TCP-ACK** y significa que el puerto es accesible, pero no se puede determinar si está abierto o cerrado.|
|`open\|filtered`|Si no obtenemos una respuesta para un puerto específico, `Nmap`Lo pondrá en ese estado. Esto indica que un firewall o un filtro de paquetes pueden proteger el puerto.|
|`closed\|filtered`|Este estado solo se produce en los escaneos **inactivos de ID IP** e indica que era imposible determinar si el puerto escaneado está cerrado o filtrado por un firewall.|

----------
### Categorias de scripts de nmap

```
sudo nmap <target> --script <script-name>,<script-name>,...
```

|**Category**|**Description**|
|---|---|
|`auth`|Determination of authentication credentials.|
|`broadcast`|Scripts, which are used for host discovery by broadcasting and the discovered hosts, can be automatically added to the remaining scans.|
|`brute`|Executes scripts that try to log in to the respective service by brute-forcing with credentials.|
|`default`|Default scripts executed by using the `-sC` option.|
|`discovery`|Evaluation of accessible services.|
|`dos`|These scripts are used to check services for denial of service vulnerabilities and are used less as it harms the services.|
|`exploit`|This category of scripts tries to exploit known vulnerabilities for the scanned port.|
|`external`|Scripts that use external services for further processing.|
|`fuzzer`|This uses scripts to identify vulnerabilities and unexpected packet handling by sending different fields, which can take much time.|
|`intrusive`|Intrusive scripts that could negatively affect the target system.|
|`malware`|Checks if some malware infects the target system.|
|`safe`|Defensive scripts that do not perform intrusive and destructive access.|
|`version`|Extension for service detection.|
|`vuln`|Identification of specific vulnerabilities.|
