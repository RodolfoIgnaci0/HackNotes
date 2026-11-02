sistema para codificar mensajes con clave privada.

ejemplo en de room en tryhackme.

//tryhackme.asc es la llave privada que se intento usar para desencriptar pero pedia contraseña, por lo que se debe hacer todo el proceso siguiente:
gpg --import tryhackme.asc
gpg --decrypt credential.pgp


//se convertira a hash con gpgjohn2
gpg2john tryhackme.asc > hashfile

//ese hashfile se pasa por john para obtener contraseña
john hashfile --wordlist=/usr/share/wordlists/rockyou.txt

//con contraseña obtenida, se desencripta el archivo encriptado.
gpg --decrypt credential.pgp