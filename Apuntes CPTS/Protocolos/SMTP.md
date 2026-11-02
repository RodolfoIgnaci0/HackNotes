Puerto 25, protocolo de mensajeria de correos, se puede interactuar usando telnet. 

Comandos:

| **Comando**  | **Descripción**                                                                                       |
| ------------ | ----------------------------------------------------------------------------------------------------- |
| `AUTH PLAIN` | AUTH es una extensión de servicio utilizada para autenticar al cliente.                               |
| `HELO`       | El cliente inicia sesión con el nombre de su computadora y, por lo tanto, inicia la sesión.           |
| `MAIL FROM`  | El cliente nombra al remitente de correo electrónico.                                                 |
| `RCPT TO`    | El cliente nombra al destinatario del correo electrónico.                                             |
| `DATA`       | El cliente inicia la transmisión del correo electrónico.                                              |
| `RSET`       | El cliente aborta la transmisión iniciada pero mantiene la conexión entre el cliente y el servidor.   |
| `VRFY`       | El cliente comprueba si un buzón está disponible para la transferencia de mensajes.                   |
| `EXPN`       | El cliente también comprueba si un buzón está disponible para la mensajería con este comando.         |
| `NOOP`       | El cliente solicita una respuesta del servidor para evitar la desconexión debido al tiempo de espera. |
| `QUIT`       | El cliente termina la sesión.                                                                         |

## Interacción
```
Rodign@htb[/htb]$ telnet 10.129.14.128 25

Trying 10.129.14.128...
Connected to 10.129.14.128.
Escape character is '^]'.
220 ESMTP Server 

HELO mail1.inlanefreight.htb

250 mail1.inlanefreight.htb

EHLO mail1

250-mail1.inlanefreight.htb
```


El comando `VRFY`Se puede utilizar para enumerar los usuarios existentes en el sistema. Sin embargo, esto no siempre funciona. Dependiendo de cómo esté configurado el servidor SMTP, el servidor SMTP puede emitir `code 252`Y confirmar la existencia de un usuario que no existe en el sistema. Una lista de todos los códigos de respuesta SMTP se puede encontrar [aquí](https://serversmtp.com/smtp-error/).
#### Telnet - VRFY
`Rodign@htb[/htb]$ telnet 10.129.14.128 25 
 Trying 10.129.14.128... 
Connected to 10.129.14.128. 
Escape character is '^]'. 
220 ESMTP Server  

VRFY root 

252 2.0.0 root`

#### Enviar un correo electrónico

```
Rodign@htb[/htb]$ telnet 10.129.14.128 25

Trying 10.129.14.128...
Connected to 10.129.14.128.
Escape character is '^]'.
220 ESMTP Server


EHLO inlanefreight.htb

250-mail1.inlanefreight.htb
250-PIPELINING
250-SIZE 10240000
250-ETRN
250-ENHANCEDSTATUSCODES
250-8BITMIME
250-DSN
250-SMTPUTF8
250 CHUNKING


MAIL FROM: <cry0l1t3@inlanefreight.htb>

250 2.1.0 Ok


RCPT TO: <mrb3n@inlanefreight.htb> NOTIFY=success,failure

250 2.1.5 Ok


DATA

354 End data with <CR><LF>.<CR><LF>

From: <cry0l1t3@inlanefreight.htb>
To: <mrb3n@inlanefreight.htb>
Subject: DB
Date: Tue, 28 Sept 2021 16:32:51 +0200
Hey man, I am trying to access our XY-DB but the creds don't work. 
Did you make any changes there?
.

250 2.0.0 Ok: queued as 6E1CF1681AB


QUIT

221 2.0.0 Bye
Connection closed by foreign host.
```