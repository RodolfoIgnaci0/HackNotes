Es una herramienta rápida y eficiente para copiar archivos de forma local y remota.
Puerto TCP 873

#### Enumeración
```
sudo nmap -sV -p 873 127.0.0.1
```
#### Interacción
```
nc -nv 127.0.0.1 873

(UNKNOWN) [127.0.0.1] 873 (rsync) open
@RSYNCD: 31.0
@RSYNCD: 31.0
#list
dev             Dev Tools
@RSYNCD: EXIT
```
#### Enumerar una acción abierta a partir de la solicitud anterior de interacción
```
rsync -av --list-only rsync://127.0.0.1/dev

receiving incremental file list
drwxr-xr-x             48 2022/09/19 09:43:10 .
-rw-r--r--              0 2022/09/19 09:34:50 build.sh
-rw-r--r--              0 2022/09/19 09:36:02 secrets.yaml
drwx------             54 2022/09/19 09:43:10 .ssh

sent 25 bytes  received 221 bytes  492.00 bytes/sec
total size is 0  speedup is 0.00
```

## Guia de como usar rsync sobre ssh
https://phoenixnap.com/kb/how-to-rsync-over-ssh