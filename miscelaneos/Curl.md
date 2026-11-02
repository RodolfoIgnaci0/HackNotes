
curl -I http://demo.ine.local -> devuelve cabeceras del sitio
curl -X OPTIONS http://demo.ine.local -v -> muestra metodos permitidos para url 
curl -X POST demo.ine.local/login.php -d "name=john&password=password" -v -> interactuando con formulario de login
curl demo.ine.local/uploads/ --upload-file hello.txt -> subir archivo (cuando esta permitido el metodo post)
curl -XDELETE demo.ine.local/uploads/hello.txt -> eliminar archivo
