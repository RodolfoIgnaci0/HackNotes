Una transferencia de zona DNS es esencialmente una copia al por mayor de todos los registros DNS dentro de una zona (un dominio y sus subdominios) de un servidor de nombre a otro
![[Pasted image 20260603175402.png]]
- `Zone Transfer Request (AXFR)`: El servidor DNS secundario inicia el proceso enviando una solicitud de transferencia de zona al servidor principal. Esta solicitud normalmente utiliza el tipo AXFR (transferencia de zona completa).
- `SOA Record Transfer`: Al recibir la solicitud (y potencialmente autenticar el servidor secundario), el servidor principal responde enviando su registro de Inicio de Autoridad (SOA). El registro SOA contiene información vital sobre la zona, incluido su número de serie, lo que ayuda al servidor secundario a determinar si los datos de su zona están actualizados.
- `DNS Records Transmission`: El servidor principal transfiere todos los registros DNS de la zona al servidor secundario, uno por uno. Esto incluye registros como A, AAAA, MX, CNAME, NS y otros que definen los subdominios del dominio, servidores de correo, servidores de nombres y otras configuraciones.
- `Zone Transfer Complete`: Una vez que se han transmitido todos los registros, el servidor principal señala el final de la transferencia de zona. Esta notificación informa al servidor secundario de que ha recibido una copia completa de los datos de la zona.
- `Acknowledgement (ACK)`: El servidor secundario envía un mensaje de confirmación al servidor principal, confirmando el recibo y procesamiento exitosos de los datos de la zona. Esto completa el proceso de transferencia de zona.
-------

#### DIG
Solicitar transferencia de zona
```
dig axfr @nsztm1.digi.ninja zonetransfer.me
```
ejercicio de htb - 10.129.17.160 es la maquina objetivo y el inlanefreight seria la zona que consulta dentro del mismo servidor dns
```
dig @10.129.17.160 axfr inlanefreight.htb
```
