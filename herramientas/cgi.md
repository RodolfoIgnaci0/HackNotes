existe la vulnerabilidad shellshock que se aprovecha de los comandos .cgi para efectuar comandos en el apache 


con msfconsole se puede usar el modulo *apache_mod_cgi_bash_env_exec*

manual:
para ejecutar, se modifica el user-agent enviando el payload que se requiera.
 en ejemplo va: () { : ; }; echo; echo; /bin/bash -c 'cat /etc/passwd'

![[Pasted image 20251226033953.png|1100]]