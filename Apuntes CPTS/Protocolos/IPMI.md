[Interfaz de gestión de plataforma inteligente](https://www.thomas-krenn.com/en/wiki/IPMI_Basics) (`IPMI`) es un conjunto de especificaciones estandarizadas para los sistemas de gestión de host basados en hardware utilizados para la gestión y supervisión de sistemas.
IPMI proporciona a los administradores de sistemas la capacidad de administrar y monitorear los sistemas, incluso si están apagados o en un estado que no responde
Los sistemas que utilizan el protocolo IPMI se denominan controladores de gestión de zócalo (BMC). Los BMC generalmente se implementan como sistemas ARM integrados que ejecutan Linux y se conectan directamente a la placa base del host. Los BMC están integrados en muchas placas base, pero también se pueden agregar a un sistema como una tarjeta PCI
***Puerto UDP 623***

### Footprinting
Nmap
```
sudo nmap -sU --script ipmi-version -p 623 ilo.inlanfreight.local
```
Metasploit
```
use auxiliary/scanner/ipmi/ipmi_version 
```
tiene opcion de crackeo dentro del mismo modulo
```
use auxiliary/scanner/ipmi/ipmi_dumphashes 
```
### Credenciales predeterminadas en algunos casos

| Producto        | Nombre de usuario | Contraseña                                                                   |
| --------------- | ----------------- | ---------------------------------------------------------------------------- |
| Dell iDRAC      | La raíz           | Calvin                                                                       |
| HP iLO          | Administrador     | Cadena aleatoria de 8 caracteres que consiste en números y letras mayúsculas |
| Supermicro IPMI | ADMIN             | ADMIN                                                                        |


