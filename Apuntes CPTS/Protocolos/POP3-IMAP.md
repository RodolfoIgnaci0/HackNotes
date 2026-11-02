PUERTOS 110 y 995 POP3 - 143 y 993 IMAP
IMAP: protocolo de red para la gestión en línea de correos electrónicos en un servidor remoto
POP3: proporciona correos electrónicos de listado, recuperación y eliminación de correos electrónicos como funciones en el servidor de correo electrónico

#### Comandos de IMAP

|**Comando**|**Descripción**|
|---|---|
|`1 LOGIN username password`|Inicio de sesión del usuario.|
|`1 LIST "" *`|Enumera todos los directorios.|
|`1 CREATE "INBOX"`|Crea un buzón con un nombre especificado.|
|`1 DELETE "INBOX"`|Elimina un buzón.|
|`1 RENAME "ToRead" "Important"`|Cambia el nombre de un buzón.|
|`1 LSUB "" *`|Devuelve un subconjunto de nombres del conjunto de nombres que el Usuario ha declarado `active`o `subscribed`.|
|`1 SELECT INBOX`|Selecciona un buzón para que se pueda acceder a los mensajes en el buzón.|
|`1 UNSELECT INBOX`|Sale del buzón seleccionado.|
|`1 FETCH <ID> all`|Recupera datos asociados a un mensaje en el buzón.|
|`1 CLOSE`|Elimina todos los mensajes con el `Deleted`Conjunto de bandera.|
|`1 LOGOUT`|Cierra la conexión con el servidor IMAP.|

#### Comandos de POP3

| **Comando**     | **Descripción**                                                            |
| --------------- | -------------------------------------------------------------------------- |
| `USER username` | Identifica al usuario.                                                     |
| `PASS password` | Autenticación del usuario usando su contraseña.                            |
| `STAT`          | Solicita el número de correos electrónicos guardados del servidor.         |
| `LIST`          | Solicita al servidor el número y tamaño de todos los correos electrónicos. |
| `RETR id`       | Solicita al servidor que entregue el correo electrónico solicitado por ID. |
| `DELE id`       | Solicita al servidor que elimine el correo electrónico solicitado por ID.  |
| `CAPA`          | Solicita al servidor que muestre las capacidades del servidor.             |
| `RSET`          | Solicita al servidor que restablezca la información transmitida.           |
| `QUIT`          | Cierra la conexión con el servidor POP3.                                   |

#### Curl
Brinda mucha info del servicio
```
curl -k 'imaps://10.129.14.128' --user cry0l1t3:1234 -v
```

## Interacción con servicio IMAP o POP3

#### openssl
```
openssl s_client -connect 10.129.14.128:pop3s
```
```
openssl s_client -connect 10.129.14.128:imaps
```

Ejemplos de interación de IMAP/IMAPS
```
a1 login robin robin                 -> login usuario
a2 list "" *                         -> listo las carpetas de la casilla de correo
a3 select inbox                      -> entro a casilla inbox
a4 search all                        -> listo si tiene correos
a5 fetch 1 (flags body[header])      -> devuelvo el encabezado del primer correo (me da el from y to)
a6 fetch 1 (flags body[text])        -> devuelvo el cuerpo del correo

aX fetch 1:* (flags body[text])      -> devuelvo todos los cuerpos de correo, empezando desde el 1
```
