# Ping

Para usar ping con solo una traza ICMP lo siguiente
- `ping -c 1 [IP]`

# Nmap
Si lo que queremos son los puertos:
-`nmap -Pn [IP]` 

Añadiendo -f podremos elegir la opcion de fast scan pero hace mucho "ruido"

-`nmap -sC -sV -oA ` 
	Con esto podremos ver los puertos y que versiones son las que se encuentran activas corriendo el servicio.



# Gobuster
Fuerza bruta de directorios. Cuando queremos ir por una web y ver si tiene directorios o rutas interesantes que podamos investigar sin perder mucho tiempo, con un wordlist por default:

`gobuster dir -u http://[IP] -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt`
