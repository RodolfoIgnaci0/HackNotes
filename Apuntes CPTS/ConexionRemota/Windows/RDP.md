Acceso remoto a ordenador que utiliza windows.
Puerto TCP/UDP 3389

#### Footprinting
```
nmap -sV -sC 10.129.201.248 -p3389 --script rdp*
```

#### Conexión (sirve xfreerdp, rdesktop o Remmina)
```
xfreerdp /u:cry0l1t3 /p:"P455w0rd!" /v:10.129.201.248
```
