Traduce nombres de dominio a IP para uso interno entre servidores.

#### Tipos de servidor dns

| Concepto DNS                | Descripción                                                                                  | Ejemplo                                                                                                                                   |
| --------------------------- | -------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| `Domain Name`               | Una etiqueta legible por humanos para un sitio web u otro recurso de Internet.               | `www.example.com`                                                                                                                         |
| `IP Address`                | Un identificador numérico único asignado a cada dispositivo conectado a Internet.            | `192.0.2.1`                                                                                                                               |
| `DNS Resolver`              | Un servidor que traduce los nombres de dominio en direcciones IP.                            | El servidor DNS de tu ISP o los resolutores públicos como Google DNS (`8.8.8.8`)                                                          |
| `Root Name Server`          | Los servidores de nivel superior en la jerarquía DNS.                                        | Hay 13 servidores root en todo el mundo, llamados A-M: `a.root-servers.net`                                                               |
| `TLD Name Server`           | Servidores responsables de dominios específicos de nivel superior (por ejemplo, .com, .org). | [Verisign](https://en.wikipedia.org/wiki/Verisign) para `.com`, [PIR](https://en.wikipedia.org/wiki/Public_Interest_Registry) para `.org` |
| `Authoritative Name Server` | El servidor que contiene la dirección IP real de un dominio.                                 | A menudo gestionado por proveedores de alojamiento o registradores de dominio.                                                            |
| `DNS Record Types`          | Diferentes tipos de información almacenada en DNS.                                           | A, AAAA, CNAME, MX, NS, TXT, etc.                                                                                                         |
#### Registros dns

| Tipo de registro | Nombre completo                   | Descripción                                                                                                                                                              | Ejemplo de archivo de zona                                                                    |
| ---------------- | --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------- |
| `A`              | Registro de dirección             | Asigna un nombre de host a su dirección IPv4.                                                                                                                            | `www.example.com.`EN A `192.0.2.1`                                                            |
| `AAAA`           | Registro de direcciones IPv6      | Asigna un nombre de host a su dirección IPv6.                                                                                                                            | `www.example.com.`EN AAAA `2001:db8:85a3::8a2e:370:7334`                                      |
| `CNAME`          | Registro de Nombre Canónico       | Crea un alias para un nombre de host, apuntándolo a otro nombre de host.                                                                                                 | `blog.example.com.`EN CNAME `webserver.example.net.`                                          |
| `MX`             | Registro de intercambio de correo | Especifica el(los) servidor(es) de correo responsable de manejar el correo electrónico para el dominio.                                                                  | `example.com.`EN MX 10 `mail.example.com.`                                                    |
| `NS`             | Registro de servidor de nombre    | Delega una zona DNS a un servidor de nombres autorizado específico.                                                                                                      | `example.com.`EN NS `ns1.example.com.`                                                        |
| `TXT`            | Registro de texto                 | Almacena información de texto arbitraria, a menudo utilizada para la verificación de dominio o políticas de seguridad.                                                   | `example.com.`EN TXT `"v=spf1 mx -all"`(Récord de SPF)                                        |
| `SOA`            | Inicio del Registro de Autoridad  | Especifica información administrativa sobre una zona DNS, incluido el servidor de nombres principal, el correo electrónico de la persona responsable y otros parámetros. | `example.com.`EN SOA `ns1.example.com. admin.example.com. 2024060301 10800 3600 604800 86400` |
| `SRV`            | Registro de servicio              | Define el nombre de host y el número de puerto para servicios específicos.                                                                                               | `_sip._udp.example.com.`EN SRV 10 5 5060 `sipserver.example.com.`                             |
| `PTR`            | Registro de puntero               | Se utiliza para búsquedas de DNS inverso, asignar una dirección IP a un nombre de host.                                                                                  | `1.2.0.192.in-addr.arpa.`EN PTR `www.example.com.`                                            |
### Herramientas

|Herramienta|Características clave|Casos de uso|
|---|---|---|
|`dig`|Herramienta versátil de búsqueda de DNS que admite varios tipos de consulta (A, MX, NS, TXT, etc.) y salida detallada.|Consultas DNS manuales, transferencias de zona (si se permite), problemas de solución de problemas DNS y análisis en profundidad de los registros DNS.|
|`nslookup`|Herramienta de búsqueda DNS más simple, principalmente para los registros A, AAAA y MX.|Consultas DNS básicas, comprobaciones rápidas de la resolución del dominio y registros del servidor de correo.|
|`host`|Herramienta de búsqueda DNS simplificada con salida concisa.|Comprobaciones rápidas de los registros A, AAAA y MX.|
|`dnsenum`|Herramienta de enumeración de DNS automatizada, ataques de diccionario, forzamiento bruto, transferencias de zona (si está permitido).|Descubrir subdominios y recopilar información de DNS de manera eficiente.|
|`fierce`|Herramienta de reconocimiento DNS y enumeración de subdominios con búsqueda recursiva y detección de comodines.|Interfaz fácil de usar para el reconocimiento DNS, la identificación de subdominios y objetivos potenciales.|
|`dnsrecon`|Combina múltiples técnicas de reconocimiento DNS y admite varios formatos de salida.|Enumeración completa de DNS, identificación de subdominios y recopilación de registros DNS para su posterior análisis.|
|`theHarvester`|Herramienta OSINT que recopila información de diversas fuentes, incluidos los registros DNS (direcciones de correo electrónico).|Recopilación de direcciones de correo electrónico, información de empleados y otros datos asociados con un dominio de múltiples fuentes.|
|`Online DNS Lookup Services`|Interfaces fáciles de usar para realizar búsquedas de DNS.|Búsquedas de DNS rápidas y fáciles, convenientes cuando las herramientas de línea de comandos no están disponibles, la comprobación de la disponibilidad del dominio o la información básica|

## Dig
|Comando|Descripción|
|---|---|
|`dig domain.com`|Realiza una búsqueda de registro A por defecto para el dominio.|
|`dig domain.com A`|Recupera la dirección IPv4 (registro A) asociada al dominio.|
|`dig domain.com AAAA`|Recupera la dirección IPv6 (registro AAA) asociada al dominio.|
|`dig domain.com MX`|Encuentra los servidores de correo (registros MX) responsables del dominio.|
|`dig domain.com NS`|Identifica los servidores de nombres autorizados para el dominio.|
|`dig domain.com TXT`|Recupera cualquier registro TXT asociado con el dominio.|
|`dig domain.com CNAME`|Recupera el registro de nombre canónico (CNAME) para el dominio.|
|`dig domain.com SOA`|Recupera el registro de inicio de autoridad (SOA) para el dominio.|
|`dig @1.1.1.1 domain.com`|Especifica un servidor de nombres específico para consultar; en este caso 1.1.1.1|
|`dig +trace domain.com`|Muestra la ruta completa de la resolución de DNS.|
|`dig -x 192.168.1.1`|Realiza una búsqueda inversa en la dirección IP 192.168.1.1 para encontrar el nombre de host asociado. Es posible que deba especificar un servidor de nombres.|
|`dig +short domain.com`|Proporciona una respuesta breve y concisa a la consulta.|
|`dig +noall +answer domain.com`|Muestra solo la sección de respuestas de la salida de consulta.|
|`dig domain.com ANY`|Recupera todos los registros DNS disponibles para el dominio (Nota: Muchos servidores DNS ignoran `ANY`Consultas para reducir la carga y prevenir el abuso, según [RFC 8482](https://datatracker.ietf.org/doc/html/rfc8482)).|
