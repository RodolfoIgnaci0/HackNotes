enumeracion de vulnerabilidades de wordpress
token api -> https://wpscan.com/profile/  -> CG0AliW5eKfs7XF0K6mgQtgKLWJ9gOXP0aizj5TqhNM
```
agrego --api-token CG0AliW5eKfs7XF0K6mgQtgKLWJ9gOXP0aizj5TqhNM
```

wpscan --url http://www.smol.thm -e vp,u,p,t

parametros de -e (enumerate)
vp -> pluggins vulnerables
u -> usuarios
p -> pluggins

-----
### Enumeración, permite devolver usuarios validos
```
wpscan --url http://127.0.0.1:80 -e
```

### Validación y fuerza bruta sobre usuario s4vitar
```
wpscan --url http://127.0.0.1:31337 -P /usr/share/wordlists/rockyou.txt -U S4vitar 
```

