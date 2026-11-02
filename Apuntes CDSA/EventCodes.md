###### Uso regular en Elasticsearch/Kibana

| Fuente         | Campo KQL         |
| -------------- | ----------------- |
| Sysmon         | `event.code`      |
| Security Audit | `winlog.event_id` |
| PowerShell     | `winlog.event_id` |
| WinRM          | `winlog.event_id` |
| Defender       | `winlog.event_id` |
| Task Scheduler | `winlog.event_id` |

# Sysmon Events (los más importantes)

|Event ID|Nombre|Qué detecta|MITRE relacionado|Prioridad|
|---|---|---|---|---|
|**1**|Process Create|Ejecución de procesos|T1059, T1204|⭐⭐⭐⭐⭐|
|**2**|File Creation Time Changed|Manipulación timestamps|T1070.006|⭐⭐|
|**3**|Network Connection|Conexiones de red de procesos|C2, lateral movement|⭐⭐⭐⭐⭐|
|**4**|Sysmon Service State Changed|Inicio/parada Sysmon|Defensa|⭐|
|**5**|Process Terminated|Terminación procesos|Defensa|⭐|
|**6**|Driver Loaded|Carga drivers|Rootkits|⭐⭐|
|**7**|Image Loaded|DLL cargadas|DLL Hijacking|⭐⭐⭐|
|**8**|CreateRemoteThread|Inyección de procesos|T1055|⭐⭐⭐⭐|
|**9**|RawAccessRead|Lectura disco bajo nivel|T1003|⭐⭐|
|**10**|Process Access|Acceso a otro proceso (LSASS)|Credential Dumping|⭐⭐⭐⭐⭐|
|**11**|File Create|Creación de archivos|Malware, herramientas|⭐⭐⭐⭐⭐|
|**12**|Registry Object Create/Delete|Cambios registro|Persistencia|⭐⭐⭐|
|**13**|Registry Value Set|Modificación valores registro|Run Keys, persistencia|⭐⭐⭐⭐⭐|
|**14**|Registry Key Rename|Manipulación registro|Persistencia|⭐⭐|
|**15**|FileCreateStreamHash|Alternate Data Streams|T1564.004|⭐⭐|
|**16**|Sysmon Config Change|Cambio configuración Sysmon|Evasion|⭐|
|**17**|Pipe Created|Named Pipes|Lateral movement|⭐⭐⭐|
|**18**|Pipe Connected|Named Pipes conexión|Lateral movement|⭐⭐⭐|
|**19**|WMI Filter Created|WMI Persistence|T1546.003|⭐⭐⭐⭐|
|**20**|WMI Consumer Created|WMI Persistence|T1546.003|⭐⭐⭐⭐|
|**21**|WMI Binding Created|WMI Persistence|T1546.003|⭐⭐⭐⭐|
|**22**|DNS Query|Consultas DNS|C2|⭐⭐⭐⭐⭐|
|**23**|File Delete|Eliminación archivos|T1070|⭐⭐⭐|
|**24**|Clipboard Change|Captura clipboard|T1115|⭐⭐|
|**25**|Process Tampering|Manipulación procesos|Evasion|⭐⭐⭐|
|**26**|File Delete Detected|Borrado archivos|T1070|⭐⭐⭐|
|**27**|File Block Executable|Bloqueo ejecución|Defensa|⭐|
|**28**|File Lock|Archivo bloqueado|Malware|⭐|
|**29**|File Executable Detected|Ejecutables|Malware|⭐⭐|
|**30**|File Creation Stream Hash|ADS|T1564|⭐⭐|

---

# PowerShell Events


Fuente:

```
Microsoft-Windows-PowerShell/Operational
```

|Event ID|Nombre|Uso|Prioridad|
|---|---|---|---|
|**4103**|Module Logging|Cmdlets usados|⭐⭐⭐|
|**4104**|Script Block Logging|Código PowerShell ejecutado|⭐⭐⭐⭐⭐|
|**4105**|ScriptBlock Start|Inicio ejecución|⭐⭐|
|**4106**|ScriptBlock End|Fin ejecución|⭐⭐|

Campos importantes:

```
powershell.file.script_block_text
winlog.user.name
host.name
```

Buscar:

```
winlog.event_id:4104 AND powershell.file.script_block_text:*Invoke-Command*
```

---

# Windows Security Events

## Autenticación

|Event ID|Nombre|Uso|
|---|---|---|
|**4624**|Successful Logon|Accesos exitosos|
|**4625**|Failed Logon|Fuerza bruta|
|**4648**|Explicit Credential Logon|Uso credenciales alternativas|
|**4672**|Special Privileges Assigned|Administrador|
|**4634**|Logoff|Cierre sesión|
|**4647**|User initiated logoff|Logout|

---

## Procesos

|Event ID|Uso|
|---|---|
|**4688**|Creación de procesos Windows|

Similar a Sysmon 1.

Buscar:

```
winlog.event_id:4688
```

---

## Persistencia

|Event ID|Uso|MITRE|
|---|---|---|
|**4698**|Scheduled Task creada|T1053|
|**4699**|Scheduled Task eliminada|T1053|
|**4700**|Task habilitada|T1053|
|**4702**|Task modificada|T1053|
|**7045**|Servicio instalado|T1543|
|**4720**|Usuario creado|T1136|
|**4732**|Usuario agregado grupo|Privilege escalation|

---

# Kerberos / Active Directory

Muy usados en ataques AD.

|Event ID|Uso|MITRE|
|---|---|---|
|**4768**|Solicitud TGT|Kerberos|
|**4769**|Service Ticket|Kerberoasting|
|**4771**|Fallo Kerberos|Password attacks|
|**4776**|Validación NTLM|Brute force|

---

# Movimiento lateral

|Event ID|Uso|
|---|---|
|**4624**|Login remoto|
|**4648**|Credenciales explícitas|
|**5140**|Acceso SMB Share|
|**5145**|Acceso detallado SMB|
|**4104**|PowerShell Remoting|
|**WinRM Event 6**|Sesión WinRM|
|**4688/Sysmon 1**|Ejecución remota|

---

# Windows Defender / Antivirus

|Event ID|Uso|
|---|---|
|**1116**|Malware detectado|
|**1117**|Acción tomada|
|**5007**|Configuración modificada|