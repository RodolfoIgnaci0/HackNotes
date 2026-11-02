Se refiere a servidores que hostean multiples sitios web, hay 3 tipos de hosting dependiendo de como funcionan para desplegar lo que se necesita:
1. basado en el fqdn, sabe que mostrar dependiendo del dato desde header html
	- www.example.com
	- www.example2.com
	- www.example3.com
2. basado en ip publica, sabe que mostrar dependiendo de la ip publica que se consulta
	- 15.0.0.1
	- 15.0.0.2
3. basado en puerto, sabe que mostrar dependiendo del puerto que se busca
	- www.example.com:80
	- www.example2.com:443
	- www.example3.com:8080
##### Gobuster
```
gobuster vhost -u http://<target_IP_address> -w <wordlist_file> --append-domain
```

#### Otras herramientas utiles
1. Feroxbuster -> no hace directamente descubrimiento de subdominios, sirve mas para buscar directorios dentro del dominio/subdominio encontrado
2. Fuff
	- ```ffuf -w wordlist.txt -u http://inlanefreight.htb:31083 -H "Host: FUZZ.inlanefreight.htb" -fs <tamaño_respuesta_falsa>```
	