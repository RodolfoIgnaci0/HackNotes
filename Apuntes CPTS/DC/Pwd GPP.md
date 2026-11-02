Para abusar de las `Contraseñas GPP`, usaremos la función [Get-GPPPassword](https://github.com/PowerShellMafia/PowerSploit/blob/master/Exfiltration/Get-GPPPassword.ps1) de `PowerSploit`, que analiza automáticamente todos los archivos XML en la carpeta Policies en `SYSVOL`, recogiendo aquellos con la propiedad `cpassword` y descifrándolos una vez detectados:

```
Import-Module .\Get-GPPPassword.ps1
Get-GPPPassword
```
![[Pasted image 20260820171620.png]]

Nota: Si sale error por no permitir ejecutar funciones de powershell, se puede modificar temporalmente
 ```
 Set-ExecutionPolicy Bypass -Scope Process -Force 
 ```
