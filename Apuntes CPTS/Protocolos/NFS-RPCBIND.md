funciona similar a smb, pero se puede montar el disco en equipo local. Funciona en puerto TCP 111 y 2049

listar servicios nfs
```
nmap --script nfs* 10.129.14.128 -sV -p111,2049
```

Mostrar acciones
```
showmount -e 10.129.14.128
```

Montura de disco en maquina local
```
Rodign@htb[/htb]$ mkdir target-NFS
Rodign@htb[/htb]$ sudo mount -t nfs 10.129.14.128:/ ./target-NFS/ -o nolock
Rodign@htb[/htb]$ cd target-NFS
Rodign@htb[/htb]$ tree .

.
└── mnt
    └── nfs
        ├── id_rsa
        ├── id_rsa.pub
        └── nfs.share

2 directories, 3 files
```

NOTA: Dependiendo de los permisos que tenga el archivo original, permitira o no modificar archivos independiente de si se cuenta con root local