sirve para generar la contraseña del archivo /etc/shadow en caso de tener permiso de escritura

```
openssl passwd -<tipo_encriptacion> -salt <valor_salt> <contraseña>

openssl passwd -1 -salt abc password
```
