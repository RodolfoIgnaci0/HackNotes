pluggin de metasploit para scan de vulnerabilidades web

uso: en msfconsole ejecutar 'load wmap'

![[Pasted image 20251226202705.png]]

agregar sitio:
wmap_sites -a 192.168.100.1

agregar target:
wmap_targets -t http://192.168.100.1

listar sitios:
wmap_sites -l

mostrar modulos a usar para scan:
wmap_run -t

ejecutar scan 
wmap_run -e

listar todas las vulnerablidades encontradas
wmap_vuln -l
