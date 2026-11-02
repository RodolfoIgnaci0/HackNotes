###################### mosquitto usado para IoT
devuelve toda la data desde sensor de temperatura a lo que busques
  mosquitto_sub -h 10.201.17.61 -t "#"

 ej: {"id":16533737979428977265,"color":"GREEN","status":"ON"}
eyJpZCI6ImNkZDFiMWMwLTFjNDAtNGIwZi04ZTIyLTYxYjM1NzU0OGI3ZCIsInJlZ2lzdGVyZWRfY29tbWFuZHMiOlsiSEVMUCIsIkNNRCIsIlNZUyJdLCJwdWJfdG9waWMiOiJVNHZ5cU5sUXRmLzB2b3ptYVp5TFQvMTVIOVRGNkNIZy9wdWIiLCJzdWJfdG9waWMiOiJYRDJyZlI5QmV6L0dxTXBSU0VvYmgvVHZMUWVoTWcwRS9zdWIifQ==

*se obtuvo el base64
 {"id":"cdd1b1c0-1c40-4b0f-8e22-61b357548b7d","registered_commands":["HELP","CMD","SYS"],"pub_topic":"U4vyqNlQtf/0vozmaZyLT/15H9TF6CHg/pub","sub_topic":"XD2rfR9Bez/GqMpRSEobh/TvLQehMg0E/sub"}

* funciona como listener
 mosquitto_sub -h 10.201.17.61 -t "U4vyqNlQtf/0vozmaZyLT/15H9TF6CHg/pub"

*funciona para preguntar cosas, en este caso al listener dio el formato de pregunta
 mosquitto_pub -h 10.201.17.61 -t "XD2rfR9Bez/GqMpRSEobh/TvLQehMg0E/sub" -m "hello"

*flag obtenida 
 mosquitto_pub -h 10.201.17.61 -t "XD2rfR9Bez/GqMpRSEobh/TvLQehMg0E/sub" -m "eyJpZCI6ICI8YmFja2Rvb3IgaWQ+IiwgImNtZCI6ICJDTUQiLCAiYXJnIjogImNhdCBmbGFnLnR4dCJ9"
