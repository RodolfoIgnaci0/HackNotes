Usa puerto TCP 3306
normalmente se usa en estructura [LAMP](https://en.wikipedia.org/wiki/LAMP_\(software_bundle\)) (Linux, Apache, MySQL, PHP)
#### Archivo de Configuración
cat /etc/mysql/mysql.conf.d/mysqld.cnf

#### Footprinting 
```
sudo nmap 10.129.14.128 -sV -sC -p3306 --script mysql*
```
#### Interacción
Sin contraseña
```
mysql -u root -h 10.129.14.132
```
Con contraseña
```
mysql -u root -pP4SSw0rd -h 10.129.14.128
```

#### Consultas importantes
| **Comando**                                          | **Descripción**                                                                                  |
| ---------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| `mysql -u <user> -p<password> -h <IP address>`       | Conéctate al servidor MySQL. **No** debe haber un espacio entre la bandera '-p' y la contraseña. |
| `show databases;`                                    | Mostrar todas las bases de datos.                                                                |
| `use <database>;`                                    | Seleccione una de las bases de datos existentes.                                                 |
| `show tables;`                                       | Mostrar todas las tablas disponibles en la base de datos seleccionada.                           |
| `show columns from <table>;`                         | Mostrar todas las columnas de la tabla seleccionada.                                             |
| `select * from <table>;`                             | Muestra todo en la tabla deseada.                                                                |
| `select * from <table> where <column> = "<string>";` | Búsqueda de la necesidad `string`En la tabla deseada.                                            |
| select version();                                    | Muestra versión de servicio.                                                                     |
