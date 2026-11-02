protocolo que sirve para monitorear dispositivos de red, manejar temas de configuracion de forma remota. version actual es SNMPv3
Puertos UDP 161 - 162

MIB
archivo de texto que todos los objketos snmp se enumeran en jerarquia de arbol. funciona para que multiples fabricantes puedan comunicarse

### Archivo de configuracion 
https://www.net-snmp.org/docs/man/snmpd.conf.html -> manual de config
```
cat /etc/snmp/snmpd.conf
```

### snmpwalk
enumerar datos //public es el string q se puede cambiar, con onesixtyone puedes obtener otro
```
snmpwalk -v2c -c public 10.129.14.128
```

Si no conocemos la cadena de la comunidad, podemos usar `onesixtyone`y `SecLists`Listas de palabras para identificar estas cadenas comunitarias.
```
sudo apt install onesixtyone
onesixtyone -c /opt/useful/seclists/Discovery/SNMP/snmp.txt 192.168.100.1
```
Una vez que conocemos una cadena comunitaria, podemos usarla con [braa](https://github.com/mteg/braa) para forzar brutamente los OID individuales y enumerar la información detrás de ellos.
```
sudo apt install braa
braa <community string>@<IP>:.1.3.6.*   # Syntax
braa public@10.129.14.128:.1.3.6.*
```