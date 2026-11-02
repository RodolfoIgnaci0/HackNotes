
Filtro xml que selecciona ID 4768 (creación de ticket kerberos) + que el tipo de encriptación sea RC4 (herramienta de ataque rubeus usa por defecto RC4)
```
<QueryList>
  <Query Id="0" Path="Security">
    <Select Path="Security">
      *[System[(EventID=4768)] and EventData[Data[@Name='TicketEncryptionType']='0x17']]
    </Select>
  </Query>
</QueryList>
```
Valor dentro de EventData > Data > TicketEncryptionType
![[Pasted image 20260820155827.png]]