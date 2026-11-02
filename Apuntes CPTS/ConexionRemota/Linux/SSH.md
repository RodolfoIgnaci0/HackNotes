Conexión remota segura
Puerto TCP 22

##### Archivo de configuración predeterminada
```
 cat /etc/ssh/sshd_config
```
--------
#### Entornos peligrosos
| **Configuración**            | **Descripción**                                  |
| ---------------------------- | ------------------------------------------------ |
| `PasswordAuthentication yes` | Permite la autenticación basada en contraseña.   |
| `PermitEmptyPasswords yes`   | Permite el uso de contraseñas vacías.            |
| `PermitRootLogin yes`        | Permite iniciar sesión como usuario root.        |
| `Protocol 1`                 | Utiliza una versión obsoleta de cifrado.         |
| `X11Forwarding yes`          | Permite el reenvío X11 para aplicaciones de GUI. |
| `AllowTcpForwarding yes`     | Permite el envío de puertos TCP.                 |
| `PermitTunnel`               | Permite la tunelización.                         |
| `DebianBanner yes`           | Muestra un banner específico al iniciar sesión.  |

-------

#### Interacción
```
ssh -v cry0l1t3@10.129.14.132 -o PreferredAuthentications=password
```