######################## Gobuster
 gobuster dir -u url -w diccionario
   ej: gobuster dir -u 10.201.67.134 -w /usr/share/seclists/Discovery/Web-Content/files.txt 
   
 gobuster dns -d url -w diccionario

-b 404,403 -> no mostrar los response code 404 y 403


------
#### fuzzing de subdominios
```
gobuster vhost -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -u http://vulnnet.thm
```
