Si lo que queremos son los puertos:
- `nmap -Pn [IP]` 

Añadiendo -f podremos elegir la opcion de fast scan pero hace mucho "ruido"

- `nmap -sC -sV ` 
	Con esto podremos ver los puertos y que versiones son las que se encuentran activas corriendo el servicio.
	`-sC` Quiere decir que el script actuará por default en cuanto a auth, broadcast y brute.
