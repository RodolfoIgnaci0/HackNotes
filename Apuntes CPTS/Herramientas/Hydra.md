Fuerza bruta a protocolo ssh, web, rdp, smb

### Uso
```
hydra -L <lista usuarios> -P <lista contraseñas> <ip> <protocolo>
hydra -l <usuarios> -p <contraseñas> <protocolo>://<ip>
```
Ejemplo
```
hydra -L user.list -P password.list ssh://10.129.42.197
```

