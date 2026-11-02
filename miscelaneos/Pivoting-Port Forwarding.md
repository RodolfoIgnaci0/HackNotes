Port forwarding en msfconsole (en meterpreter de equipo intermedio, ya vulnerado)
run autoroute -s ip_equipo_entre_redes_ip_rango_nuevo

arp -a  ->  scan de otras redes que lleguen

------

Comunicarse desde el equipo atacante hacia pc no directamente accesible.

1.- En metasploit realizar un autoroute 
```
run autoroute -s ip_equipo_con_segmento_que_no_se_llega
```
NOTA: con esto ya se pueden usar modulos de metasploit en host que antes no se llegaba.

se pueden hacer tuneles desde meterprete
```
portfwd add -l local_port -p target_port -r target_ip
portfwd add -l 1234 -p 80 -r 10.2.27.187
```

una vez hecho, puedo usar nmap para obtener detalle del servicio corriendo
```
db_nmap -sS -sCV -p 1234 localhost ó nmap -sS -sCV -p 1234 localhost
```

-------

2.- se usará el aplicativo proxychains, y hay que fijarse al final del archivo adjunto, que puerto utiliza
```
cat /etc/proxychains4.conf
	socks 127.0.0.1 9050
```

3.- dentro de metasploit buscamos por el modulo auxiliary/server/socks_proxy
	seteamos el puerto del paso anterior y la version 
```
set SRVPORT 9050
set VERSION 4a 
exploit
```

4.- con esto hecho, se pueden realizar consultas desde equipo atacante anteponiendo "proxychains"
```
proxychains nmap demo1.ine.local -sT -Pn -sV -p 445
```

