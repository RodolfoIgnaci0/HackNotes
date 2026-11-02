Los R-Services son un conjunto de servicios alojados para habilitar el acceso remoto o emitir comandos entre hosts Unix a través de TCP/IP. Los r-servicios transmiten información de cliente a servidor (y viceversa.) a través de la red en un formato no cifrado, haciendo posible que los atacantes intercepten el tráfico de red
Puertos 512, 513 y 514

La suite [R-commands](https://en.wikipedia.org/wiki/Berkeley_r-commands) consta de los siguientes programas:

- rcp (`remote copy`)
- Rexec (`remote execution`)
- rlogin (`remote login`)
- rsh (`remote shell`)
- Rstat
- Ruptime
- rwho (`remote who`)
#### Comandos mas abusados

| **Comando** | **Servicio Daemon** | **Puerto** | **Protocolo de transporte** | **Descripción**                                                                                                                                                                                                                                                                                                                                              |
| ----------- | ------------------- | ---------- | --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `rcp`       | `rshd`              | 514        | TCP                         | Copie un archivo o directorio bidireccionalmente desde el sistema local al sistema remoto (o viceversa) o de un sistema remoto a otro. Funciona como el `cp`Comando en Linux pero proporciona `no warning to the user for overwriting existing files on a system`.                                                                                           |
| `rsh`       | `rshd`              | 514        | TCP                         | Abre un shell en una máquina remota sin un procedimiento de inicio de sesión. Se basa en las entradas de confianza en el `/etc/hosts.equiv`y `.rhosts`Archivos para validación.                                                                                                                                                                              |
| `rexec`     | `rexecd`            | 512        | TCP                         | Permite a un usuario ejecutar comandos de shell en un equipo remoto. Requiere autenticación mediante el uso de un `username`y `password`A través de un socket de red no cifrado. La autenticación es anulada por las entradas de confianza en el `/etc/hosts.equiv`y `.rhosts`Archivos.                                                                      |
| `rlogin`    | `rlogind`           | 513        | TCP                         | Permite a un usuario iniciar sesión en un host remoto a través de la red. Funciona de manera similar a `telnet`Pero solo puede conectarse a hosts similares a Unix. La autenticación es anulada por las entradas de confianza en el `/etc/hosts.equiv`y `.rhosts`Archivos.  ambos archivos guardan host que serán de confianza para acceder sin contraseñas. |

------
#### Footprinting
```
sudo nmap -sV -p 512,513,514 10.0.17.2
```

#### Interacción con rlogin
```
rlogin 10.0.17.2 -l htb-student
```
##### Esto es posible porque en configuración de archivo .rhosts esta disponible para acceso sin contraseña (los + son wildcards)
```
cat .rhosts

htb-student     10.0.17.2
+               10.0.17.10
+               +
```
