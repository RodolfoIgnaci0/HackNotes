Tipos de DNS

|**Tipo de servidor**|**Descripción**|
|---|---|
|`DNS Root Server`|Los servidores raíz de los DNS son responsables de los dominios de nivel superior (`TLD`). Como última instancia, solo se solicitan si el servidor de nombres no responde. Por lo tanto, un servidor raíz es una interfaz central entre los usuarios y el contenido en Internet, ya que vincula el dominio y la dirección IP. La [Corporación de Internet para Nombres y Números Asignados](https://www.icann.org/) (`ICANN`) coordina el trabajo de los servidores de nombres raíz. Hay `13`Tales servidores raíz en todo el mundo.|
|`Authoritative Nameserver`|Los servidores de nombres autorizados tienen autoridad para una zona en particular. Solo responden a las consultas de su área de responsabilidad y su información es vinculante. Si un servidor de nombres autorizado no puede responder a la consulta de un cliente, el servidor de nombres raíz se hace cargo en ese punto. Basado en el país, la empresa, etc., los servidores de nombres autorizados proporcionan respuestas a los servidores de nombres DNS recursivos, ayudando a encontrar el servidor web específico (s).|
|`Non-authoritative Nameserver`|Los servidores de nombres no autorizados no son responsables de una zona DNS en particular. En su lugar, recopilan información sobre zonas DNS específicas, lo que se realiza mediante consultas DNS recursivas o iterativas.|
|`Caching DNS Server`|Almacenamiento en caché de servidores DNS de información de caché de otros servidores de nombres durante un período específico. El servidor de nombres autorizado determina la duración de este almacenamiento.|
|`Forwarding Server`|Los servidores de reenvío realizan una sola función: reenvían consultas DNS a otro servidor DNS.|
|`Resolver`|Los solucionadores no son servidores DNS autorizados, sino que realizan la resolución de nombres localmente en el equipo o el router.|

Tipos de consulta

|**Registro DNS**|**Descripción**|
|---|---|
|`A`|Devuelve una dirección IPv4 del dominio solicitado como resultado.|
|`AAAA`|Devuelve una dirección IPv6 del dominio solicitado.|
|`MX`|Devuelve los servidores de correo responsables como resultado.|
|`NS`|Devuelve los servidores DNS (servidores de nombres) del dominio.|
|`TXT`|Este registro puede contener información variada. El todoterreno se puede utilizar, por ejemplo, para validar la Google Search Console o validar certificados SSL. Además, las entradas SPF y DMARC están configuradas para validar el tráfico de correo y protegerlo del spam.|
|`CNAME`|Este registro sirve como un alias para otro nombre de dominio. Si desea que el dominio [www.hackthebox.eu](http://www.hackthebox.eu) apunte a la misma IP que hackthebox.eu, crearía un registro A para hackthebox.eu y un registro CNAME para [www.hackthebox.eu](http://www.hackthebox.eu).|
|`PTR`|El registro PTR funciona al revés (búsqueda inversa). Convierte las direcciones IP en nombres de dominio válidos.|
|`SOA`|Proporciona información sobre la zona DNS correspondiente y la dirección de correo electrónico del contacto administrativo.|
```
dig soa www.inlanefreight.com
```

Archivos de configuracion comunes
```
root@bind9:~# cat /etc/bind/named.conf.local
```
- `named.conf.local`
- `named.conf.options`
- `named.conf.log`
archivo de zona
```
cat /etc/bind/db.domain.com
```

### Consultas a DNS

```
dig ns inlanefreight.htb @10.129.14.128
```
muestra version de dns
```
dig CH TXT version.bind @10.129.120.85
```
Muestra todas las entradas disponibles
```
dig any inlanefreight.htb @10.129.14.128
```
muestra datos de transferencia de zona axfr (dns primario - secundario), a partir de ahi se puede usar los mismos registros que te brinda para volver a usar misma consulta con ej hacia internal.inlanefreight.htb
```
dig axfr inlanefreight.htb @10.129.14.128
```



## Herramientas
#### DNSEnum
```
dnsenum --dnsserver 10.129.14.128 --enum -p 0 -s 0 -o subdomains.txt -f /opt/useful/seclists/Discovery/DNS/subdomains-top1million-110000.txt inlanefreight.htb
```


