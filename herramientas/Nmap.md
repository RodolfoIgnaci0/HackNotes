lista de scripts de nmap
```
/usr/share/nmap/scripts
```

forma de pasar parametros
```
nmap -sV -p 80 --script=http-shellshock --script-args "http-shellshock.uri=/gettime.cgi" 192.152.25.3
```

