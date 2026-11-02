Aplicativo para desencriptar.

john hash.txt --format=NT --wordlist=/usr/share/wordlist/rockyou.txt

------
### Crackear zip

Crear un hash del zip con contraseña
```
zip2john backup.zip > hash.txt
```

hash creado se desencripta ya de forma normal con john
```
john hash.txt
```
