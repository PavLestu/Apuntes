# JSON
No entiendo por qué a la hora de formar un json, lo lógico seria formarlo de la siguiente manera, si hemos optado por poner `Content-Type: application/json`:
- `{"username":"manolo", "perro":"Esteban"}`
Pero a la hora de realizar un post nos ha resultado como que no recive nada si no lo hacemos de esta manera:
- `{"username":{"$ne":"admin"}, "password":{"$ne":"pass"}}`
	Por qué el `$ne` ??
	
	
	# Entendido!!!
	Por lo visto es porque es un truco conocido para hacer un bypass en SQLite!
	- Investigar un poco más!


# Flags
Por ahora todas las flags que pillamos siempre se encuentran en /root/root.txt 
Es algo normal o solo para este jueguillo por ahora?

