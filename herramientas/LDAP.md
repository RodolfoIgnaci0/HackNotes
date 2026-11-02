####################### LDAP
Enumeracion 
 ldapsearch -x -H ldap://host_ip -s base
   -x: Autenticación anónima.
   -H: Especifica el servidor LDAP.
   -s: Limita la consulta sólo al objeto base y no busca subárboles

 ldapsearch -x -H ldap://10.211.11.10 -b "dc=tryhackme,dc=loc" "(objectClass=person)" 

####################### Enumerar usuarios con RCP
 rpcclient -U "" 10.211.11.10 -N
    -dentro de la shell generada, se usa enumdomusers para listar usuarios

####################### determinar politicas de contraseñas
 crackmapexec smb 10.211.11.10 --pass-pol
