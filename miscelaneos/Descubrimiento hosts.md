	### Descubrimiento de hosts

```
fping -a -g {Rango de IP} 
```

- -a: Este argumento indica que muestre solamente las ips que están activas en la red.
- -g: Este argumento especifica que vamos a hacer el ping a un rango de ip.

```
nmap -sn {Rango de IP}
```

- -sn Este argumento indica a nmap que realice un escaneo de ping al rango de ip indicado.

```
netdiscover -r {Rango de IP}
```

- -r Este argumento indica que se va escanear un rango de ip.