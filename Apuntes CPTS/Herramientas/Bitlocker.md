#### Montar una unidad en linux
```
Rodign@htb[/htb]$ sudo apt-get install dislocker
```
se crean carpetas donde se montara el disco
```
Rodign@htb[/htb]$ sudo mkdir -p /media/bitlocker
Rodign@htb[/htb]$ sudo mkdir -p /media/bitlockermount
```
usamos losetup para configurar el VHD como [loop device](https://en.wikipedia.org/wiki/Loop_device), desencriptar la unidad usando dislocker, y finalmente montar el disco
```
Rodign@htb[/htb]$ sudo losetup -f -P Backup.vhd

Rodign@htb[/htb]$ sudo losetup -j Backup.vhd -> entrega el /dev/loop asociado a particion
Rodign@htb[/htb]$ lsblk -f /dev/loop0 -> con input anterior, vemos en que bloque quedo

Rodign@htb[/htb]$ sudo dislocker /dev/loop0p2 -u1234qwer -- /media/bitlocker
Rodign@htb[/htb]$ sudo mount -o loop /media/bitlocker/dislocker-file /media/bitlockermount
```
si todo funcionó se navega al disco
```
Rodign@htb[/htb]$ cd /media/bitlockermount/
Rodign@htb[/htb]$ ls -la
```

#### Desmontar
```
Rodign@htb[/htb]$ sudo umount /media/bitlockermount
Rodign@htb[/htb]$ sudo umount /media/bitlocker
```