herramienta de descifrado de contraseñas (password cracking) para Linux, Windows y macOS
Listado de hashes: https://hashcat.net/wiki/doku.php?id=example_hashes

```
 hashcat -a 0 -m 0 <hashes> [wordlist, rule, mask, ...]
```
- `-a` se utiliza para especificar el `modo de ataque` (attack mode)
- `-m` se utiliza para especificar el `tipo de hash` (hash type)
- `<hashes>` es una cadena de hash o un archivo que contiene uno o más hashes de contraseñas del mismo tipo
- `[wordlist, rule, mask, ...]` es un marcador de posición para argumentos adicionales que dependen del modo de ataque


### Opciones del -a
- 0 : modo diccionario -> hashcat -a 0 -m 0 e3e3ec5831ad5e7288241960e5d4fdb8 /usr/share/wordlists/rockyou.txt
- 3 : ataque de mascara -> si sabemos que una contraseña tiene ocho caracteres de longitud, en lugar de probar todas las combinaciones posibles, podríamos definir una máscara que pruebe combinaciones de seis letras seguidas de dos números. Una máscara se define combinando una secuencia de símbolos, donde cada uno representa un conjunto de caracteres integrado o personalizado. Hashcat incluye varios conjuntos de caracteres integrados:

Contraseñas que comiencen con una letra mayúscula, continúen con cuatro letras minúsculas, un dígito y luego un símbolo
```
hashcat -a 3 -m 0 1e293d6912d074c0fd15844d803400dd '?u?l?l?l?l?d?s'
```

|Símbolo|Conjunto de caracteres|
|---|---|
|?l|abcdefghijklmnopqrstuvwxyz|
|?u|ABCDEFGHIJKLMNOPQRSTUVWXYZ|
|?d|0123456789|
|?h|0123456789abcdef|
|?H|0123456789ABCDEF|
|?s|«espacio»!"#$%&'()*+,-./:;<=>?@[]^_`{|
|?a|?l?u?d?s|
|?b|0x00 - 0xff|
### Rules
realiza modificaciones específicas en las contraseñas y así generar aún más intentos. Los archivos de reglas que vienen con hashcat se encuentran normalmente en `/usr/share/hashcat/rules`
```
hashcat -a 0 -m 0 1b0556a75770563578569ae21392630c /usr/share/wordlists/rockyou.txt -r /usr/share/hashcat/rules/best64.rule
```
##### Creación de reglas
https://hashcat.net/wiki/doku.php?id=rule_based_attack

| **Function** | **Description**                                  |
| ------------ | ------------------------------------------------ |
| `:`          | Do nothing                                       |
| `l`          | Lowercase all letters                            |
| `u`          | Uppercase all letters                            |
| `c`          | Capitalize the first letter and lowercase others |
| `sXY`        | Replace all instances of X with Y                |
| `$!`         | Add the exclamation character at the end         |
```
cat custom.rule
:
c
so0
c so0
sa@
c sa@
c sa@ so0
```

se genera nuevo diccionario aplicando las reglas configuradas en el custom.rule. (password.list es el diccionario base y el final sera mut_password.list)
```
hashcat --force password.list -r custom.rule --stdout | sort -u > mut_password.list
```