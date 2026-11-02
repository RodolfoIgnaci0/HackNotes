
### Commandos base de ftp

| **Comandos** | **Descripción**                                                                                                                                     |
| ------------ | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| `connect`    | Establece el host remoto, y opcionalmente el puerto, para las transferencias de archivos.                                                           |
| `get`        | Transfiere un archivo o un conjunto de archivos desde el host remoto al host local.                                                                 |
| `put`        | Transfiere un archivo o un conjunto de archivos desde el host local al host remoto.                                                                 |
| `quit`       | Salidas tftp.                                                                                                                                       |
| `status`     | Muestra el estado actual de tftp, incluyendo el modo de transferencia actual (ascii o binario), estado de conexión, valor de tiempo de espera, etc. |
| `verbose`    | Activa o desactiva el modo verbose, que muestra información adicional durante la transferencia de archivos.                                         |

Descarga masiva desde un ftp
```
wget -m --no-passive ftp://anonymous:anonymous@10.129.14.136
```


#### Conexión a FTP que usa SSL
```
openssl s_client -connect 10.129.14.136:21 -starttls ftp
```



------
### Configuración de vsftpd
```
Rodign@htb[/htb]$ cat /etc/vsftpd.conf | grep -v "#"
```

|**Configuración**|**Descripción**|
|---|---|
|`listen=NO`|¿Huir de lo inetd o como un demonio independiente?|
|`listen_ipv6=YES`|¿Escuchar en IPv6?|
|`anonymous_enable=NO`|¿Habilitar el acceso anónimo?|
|`local_enable=YES`|¿Permitir que los usuarios locales inicien sesión?|
|`dirmessage_enable=YES`|¿Mostrar mensajes de directorio activos cuando los usuarios entran en ciertos directorios?|
|`use_localtime=YES`|¿Usar la hora local?|
|`xferlog_enable=YES`|¿Activar el registro de cargas/descargas?|
|`connect_from_port_20=YES`|¿Conectar desde el puerto 20?|
|`secure_chroot_dir=/var/run/vsftpd/empty`|Nombre de un directorio vacío|
|`pam_service_name=vsftpd`|Esta cadena es el nombre del servicio PAM que usará vsftpd.|
|`rsa_cert_file=/etc/ssl/certs/ssl-cert-snakeoil.pem`|Las tres últimas opciones especifican la ubicación del certificado RSA para usar para conexiones cifradas SSL.|
|`rsa_private_key_file=/etc/ssl/private/ssl-cert-snakeoil.key`||
|`ssl_enable=NO`|
Además, hay un archivo llamado `/etc/ftpusers`A la que también debemos prestar atención, ya que este archivo se utiliza para denegar a ciertos usuarios el acceso al servicio FTP. En el siguiente ejemplo, los usuarios `guest`, `john`, y `kevin`No se les permite iniciar sesión en el servicio FTP, incluso si existen en el sistema Linux.

#### Categoría: FTPUS

        Sesión de conchas
`Rodign@htb[/htb]$ cat /etc/ftpusers guest john kevin`

### Config uso anonimo

| **Configuración**              | **Descripción**                                                                  |
| ------------------------------ | -------------------------------------------------------------------------------- |
| `anonymous_enable=YES`         | ¿Permitir el inicio de sesión anónimo?                                           |
| `anon_upload_enable=YES`       | ¿Permitiendo que los anónimos carguen archivos?                                  |
| `anon_mkdir_write_enable=YES`  | ¿Permitir que el anonimato cree nuevos directorios?                              |
| `no_anon_password=YES`         | ¿No pides contraseña anónima?                                                    |
| `anon_root=/home/username/ftp` | Directorio para anónimos.                                                        |
| `write_enable=YES`             | ¿Permitir el uso de comandos FTP: STOR, DELE, RNFR, RNTO, MKD, RMD, APPE y SITE? |