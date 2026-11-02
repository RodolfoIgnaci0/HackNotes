Es el sistema de gestión de base de datos relacional basado en SQL de Microsoft. Puerto TCP predeterminado 1433
#### Herramientas utiles para usar
- [Mssql-cli](https://docs.microsoft.com/en-us/sql/tools/mssql-cli?view=sql-server-ver15) 
- [SQL Server PowerShell](https://docs.microsoft.com/en-us/sql/powershell/sql-server-powershell?view=sql-server-ver15) 
- [HeidiSQL](https://www.heidisql.com) 
- [SQLPro](https://www.macsqlclient.com) 
- [Impacket's mssqlclient.py](https://github.com/SecureAuthCorp/impacket/blob/master/examples/mssqlclient.py) 
-------
#### Usuario por defecto
```
NT SERVICE\MSSQLSERVER
```

Windows subyacente procesará la solicitud de inicio de sesión y utilizará la base de datos SAM local o el controlador de dominio (que aloja Active Directory) antes de permitir la conectividad al sistema de administración de bases de datos

----------
### Footprinting

#####  script de nmap
```
sudo nmap --script ms-sql-info,ms-sql-empty-password,ms-sql-xp-cmdshell,ms-sql-config,ms-sql-ntlm-info,ms-sql-tables,ms-sql-hasdbaccess,ms-sql-dac,ms-sql-dump-hashes --script-args mssql.instance-
```
##### metasploit
```
scanner/mssql/mssql_ping
```
##### conexion con impacket
```
python3 mssqlclient.py Administrator@10.129.201.248 -windows-auth
```

#### Queries utiles
Lista tablas -> SELECT name FROM sys.tables;
Listar bases de datos -> SELECT * FROM information_schema.tables;

