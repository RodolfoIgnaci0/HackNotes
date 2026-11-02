Herramienta para desencriptar
Samples de encriptación:
- https://pentestmonkey.net/cheat-sheet/john-the-ripper-hash-formats
- https://openwall.info/wiki/john/sample-hashes
#### Uso entregando el formato
`john --format=<formato> <hash_file>`
#### Modo Single
archivo passwd, El modo Single crack utilizará esta información para generar contraseñas candidatas y probarlas contra el hash
```
r0lf:$6$ues25dIanlctrWxg$nZHVz2z4kCy1760Ee28M1xtHdGoy0C2cYzZ8l2sVa1kIa8K9gAcdBP.GI6ng/qA4oaMrgElZ1Cb9OeXO4Fvy3/:0:0:Rolf Sebastian:/home/r0lf:/bin/bash
```
uso
```
john --single passwd
```

#### Modo wordlist
```
john --wordlist=<wordlist_file> <hash_file>
```

#### Modo incremental
Utiliza el modelo estadistico de Markov, probando todas las combinaciones. genera dinamicamente las contraseñas a probar *mucho mas exhaustivo y demorado*
```
john --incremental <hash_file>
```

*Nota: por defecto john the ripper usa modo incremental definido en archivo john.conf*

## Herramientas incluidas con john para descifrar archivos (algunas)

| **Herramienta**         | **Descripción**                                    |
| ----------------------- | -------------------------------------------------- |
| `pdf2john`              | Convierte documentos PDF para John                 |
| `ssh2john`              | Convierte claves privadas SSH para John            |
| `mscash2john`           | Convierte hashes de MS Cash para John              |
| `keychain2john`         | Convierte archivos keychain de OS X para John      |
| `rar2john`              | Convierte archivos RAR para John                   |
| `pfx2john`              | Convierte archivos PKCS#12 para John               |
| `truecrypt_volume2john` | Convierte volúmenes de TrueCrypt para John         |
| `keepass2john`          | Convierte bases de datos de KeePass para John      |
| `vncpcap2john`          | Convierte archivos PCAP de VNC para John           |
| `putty2john`            | Convierte claves privadas de PuTTY para John       |
| `zip2john`              | Convierte archivos ZIP para John                   |
| `hccap2john`            | Convierte capturas de handshake WPA/WPA2 para John |
| `office2john`           | Convierte documentos de MS Office para John        |
| `wpa2john`              | Convierte handshakes WPA/WPA2 para John            |
| ...SNIP...              | ...SNIP...                                         |
