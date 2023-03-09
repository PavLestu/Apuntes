Esta herramienta generalmente vamos a usarla para encontrar directorios de un servicio web `http://[example.com]/{gobuster}` , ahorrandonos mucho tiempo metiendo las palabras que por default pueden tener algun directorio en las paginas web. `/admin` `/login` etc

Importante no olvidarse del `/` al final del link porque si no es muy probable que no funcione adecuadamente (ultima máquina nos ocurrio[soccer]).

## Cosillas a tener en cuenta

Para usarlo con una wordlist por defecto que no taradará "mucho":
- `gobuster dir -u http://[IP]/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt`
Pero tengamos en cuenta que esto no nos encontrará cosas como `dev.[loquesea].htb` para eso usaremos:

- `gobuster vhost -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -u stocker.htb/ -t 50 
	(vhost virtual host brute-force mode)
	(con el argumento t definimos el numero de hilos que vamos a usar. Default =10)



