wfuzz -c --hc=403 --sc=200 -t20 -w /usr/share/Seclist/discovery/file.txt -H "Host: FUZZ.tinder.com" http://tinder.com

wfuzz -c --hc=403 --sc=200 -t20 -w /usr/share/Seclist/discovery/file.txt  http://tinder.com/FUZZ

Scan por extensión (valido para 1 tipo):
wfuzz -c --hc=403 --sc=200 -t20 -w /usr/share/Seclist/discovery/file.txt  http://tinder.com/FUZZ.html

Scan por extensión (valido para varios tipo, segundo fuzz es fuz2z):
wfuzz -c --hc=403 --sc=200 -t20 -w /usr/share/Seclist/discovery/file.txt  -z list,html-php http://tinder.com/FUZZ.FUZ2Z


hide code -> --hc=404
show code -> --sc=200
output en colores -> -c


hace un scan cambiando el id en el rango dado (tipo sniper de burpsuite)
wfuzz -c -t 200 -z range,1-20000 'https://www.mi.com/details?product_id=FUZZ'
