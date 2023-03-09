## Namp
	- 22/tcp OpenSSH 8.2 Ubuntu
	- 80/tcp http 1.18.0
	- 9091/tcp open xmltec-xmlmail?

# Gobuster

Cuidado aqui! Debemos de pensar bien lo que queremos. En principio siempre queremos ir a por los directorios en primera instancia. Ergo:
![[Pasted image 20230303160238.png]]
Tenemos un directorio `tiny` asi que iremos a ver que nos arroja

![[Pasted image 20230303163203.png]]
Tienen un gestor de archivos. si investigamos un poco sabemos que tienen user por default. Por lo que podemos intentarlo:

![[Pasted image 20230303163419.png]]

![[Pasted image 20230303170554.png]]

Somos admins. Ahora, deberemos meter solo una rev shell en php. 

En principio usaremos alguna ya hecha y sencilla:

-![[Pasted image 20230306141442.png]]
 
Una vez hecho esto, ejecutamos `nc -lvnp [PORT]`:
![[Pasted image 20230306141621.png]]

Ahora trataremos de escalar privilegios
![[Pasted image 20230306141834.png]]

Lo insertamos de nuevo en /etc/hosts para poder acceder. Y como siempre que encontramos una nueva url, puede ser suceptible de tener nuevas rutas, asi que  probamos de nuevo con gobuster 
- `gobuster dir -u soc-player.soccer.htb/ -w /usr/share/wordlists/dirbuster/directory-medium-2.3.txt -t 50`

Nada más arrancar, somos conscientes de varios status 200 (que a priori son los que más nos interesan):
![[Pasted image 20230306143232.png]]

Siguiendo la lógica, lo más probable es que la mejor ruta a seguir por ahora es check:

![[Pasted image 20230306143326.png]]

Parece que debemos de estar logueados. Vamos a singup y le metemos las credenciales que sean:
![[Pasted image 20230306143750.png]]


-seguiremos en otro momento. Por ahora deberemos hacer una entrada a los tickets y ver por curl o burpsuite que usa para mandar la info-
