ver privilegios de shell
```
cat /etc/shells | while read shell; do ls -l $shell 2>/dev/null; done
```

![[Pasted image 20260122003851.png]]

------
### Ver conexiones activas
```
netstat -tulnp
```