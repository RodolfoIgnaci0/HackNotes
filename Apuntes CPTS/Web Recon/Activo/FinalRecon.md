script en python que automatiza reconocimiento en sitios web, entrega certificados, correos, dmarc, enumeracion dns, subdomions, etc.
##### Instalación
```
Rodign@htb[/htb]$ git clone https://github.com/thewhiteh4t/FinalRecon.git
Rodign@htb[/htb]$ cd FinalRecon
Rodign@htb[/htb]$ pip3 install -r requirements.txt
Rodign@htb[/htb]$ chmod +x ./finalrecon.py
Rodign@htb[/htb]$ ./finalrecon.py --help
```

##### Devuelve headers y whois del sitio
```
./finalrecon.py --headers --whois --url http://inlanefreight.com
```

