 # Procedimiento normal
  `ping -c 1 10.10.11.196`
- `ttl=63` intuimos Linux
`nmap -Pn 10.10.11.196`
- ssh 22
- http 80

![[Pasted image 20230228143504.png]]
Como siempre que vemos un servicio web, modificamos el fichero hosts para poder acceder a el desde el navegador y ver que tenemos.
![[Pasted image 20230228143720.png]]

Como siempre que encontramos una web, queremos ver que directorios pueden sernos utiles,  dado que no vemos nada en el js por ahora. 

Usamos gobuster para encontrar directorios.
![[Pasted image 20230228162933.png]]
Lamentablemente no vamos encontrando nada significante por el momento, asi que vamos a hacer uso de la opcion vhost.
![[Pasted image 20230228163118.png]]
Bingo! tenemos una respuesta 302, lo que nos quiere decir que hay un recurso movido.

No tenemos mucha idea de que hacer en estos casos, pero por lo visto se procede de la misma manera que con la web. Editamos el `/etc/hosts` .

![[Pasted image 20230228163850.png]]
De nuevo, bingo! Lo que se me ocurriria es probar admin admin o cualquier combinacion facil, y así mirar la respuesta que nos arroja.

![[Pasted image 20230228223841.png]]
No nos responde mal, tenemos algo, pero nos arroja un error. Lo intentamos cambiando el content-type por `application/json`, pero no sabemos por qué nos responde mal o no nos reconoce que sea JSON.
![[Pasted image 20230228224001.png]]
![[Pasted image 20230228224019.png]]
Nos devuelve un 404, pero creeo que es porque en la opción `Accept` en la request POST no nos deja application/json, aunque lo cambiemos. 

Debido a esto, tiramos de `curl`:

Tras mucho indagar, sabemos que para las bbdd noSQL podemos tratar de hacer un injection haciendo uso de lo siguiente en JSON:
- ``{"username":{"$ne":"admin"}, "password":{"$ne":"pass"}}``

Por lo que el curl que nos quedará será:

- `curl -X POST dev.stocker.htb/login -H 'COntent-Type: application/json' -d '{"username":{"$ne":null},"password":{"$ne":null}} -v'`
![[Pasted image 20230228235413.png]]
![[Pasted image 20230301000250.png]]

#### Tenemos acceso a `/stock`
Para iniciar sesion en el navegador debemos de copiar la cookie y pegarla en el storage de la siguiente manera:
![[Pasted image 20230301001933.png]]

Bingo!
![[Pasted image 20230301001947.png]]
Ahora necesitamos un proxy para poder interceptar los paquetes cuando mandemos algo al basket y demos a realizar compra. Usaremos Burp:

![[Pasted image 20230301003328.png]]

Ahora nos generará un pdf:
![[Pasted image 20230301003420.png]]

Nota para continuar: no debemos de meter un iframe en title tratando de acceder a /etc/users a ver que pasa
`Esta técnica es practicamente un xss. Para este tipo de tecnicas igual que para interceptar el tráfico podemos hacer uso de BurpSuite. Pero deberemos de mejorar en este aspecto para no solo estar pendientes del burp siempre que queramos hacer xss`


![[Pasted image 20230302165429.png]]
Le mandamos esa reques POST en la que le pedimos que en el title nos de un iframe con la info de /etc/passwd a ver si rascamos algo.

![[Pasted image 20230302165528.png]]
En principio nos da 200 por lo que está hecho el pdf. Como al arrojarnos el archivo pdf nos indica `/api/po/[orderId]` metemos nuestro nuevo orderID para que nos arroje el nuevo:
![[Pasted image 20230302165807.png]]
Para leer mejor modificamos el css dentro de la etiqueta.
![[Pasted image 20230302170645.png]]

Sabemos que usa mongodb.  Así que de manera análoga, vamos a tratar de acceder al index.js a ver si es en esta página donde se conecta a la bbdd con user y pass:

![[Pasted image 20230302171116.png]]
No es nada fiable, pero tirar de Angoose como el usuario de la base de datos parece hasta una mala broma...pero es que seguramente que será asi para la máquina y por lo que hemos visto en algun writeup, es así... Asi que iremos a tiro hecho.

![[Pasted image 20230302171438.png]]
Estamos dentro. Veremos que permisos tenemos y que podemos hacer 
![[Pasted image 20230302171736.png]]
Este usuario puede ejecutar lo que quiera de esa carpeta siempre que sea `*.js` asi que pensaremos in script que acceda a root/root.txt y capturaremos el hash.

![[Pasted image 20230302182049.png]]
![[Pasted image 20230302182107.png]]
Done!
