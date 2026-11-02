Busca de link en link de sitio por información que parezca importante como api key, correos, etc.
hay 2 tipos de crawling, el que se mete por nivel de directorio mapeando por profundidad y otro que toma una carpeta y entra hasta lo maximo posible para luego cambiar a otra y asi mapear directorio entero.


## ReconSpider
#### Instalación
```
pip3 install scrapy  
wget -O ReconSpider.zip https://academy.hackthebox.com/storage/modules/144/ReconSpider.v1.2.zip  
unzip ReconSpider.zip  
```
#### Uso
```
python3 ReconSpider.py http://dev.web1337.inlanefreight.htb:34677  
cat results.json
```