Inyección de codigo JS en aplicaciones Web. Existen tres tipos de xss. 

Para evitar cualquiera de los ataques que expondremos a continuación, con una simple validación de los datos antes de ser tratados, podremos evitarlo.

## XSS Reflejado

Este tipo de ataque se realiza en una página que sabemos que se puede inyectar codigo por la URL. Una vez modificada la URL, el valor se verá en la página. Como los mensajes como <Hola [nombre por URL]>
	
- ``https://insecure-website.com/search?term=gift``
Se reflejará algo como:
- `<p>You searched for: gift</p>`


## XSS Persistente

Es el más utilizado. Esto no solo se va a ejecutar para el cliente concreto. Va a ser visible para todo aquel que visite la página. 

Esto se puede hacer por ejemplo inyectándo codigo en un comentario, un pdf,  etc. Algo que sea persistente dentro del server.

## XSS DOM

```
Si no hay una regulación suficiente de los _inputs_ del usuario, este puede ejecutar código en el navegador por medio del DOM de un sitio web. **Dado que el DOM se ejecuta en memoria**, permite ejecutar código malicioso sin recurrir a los dos métodos mencionados previamente.

El código malicioso en un XSS basado en DOM también puede incrustarse en la URL y enviársele a una víctima. No obstante, **la vulnerabilidad se encuentra en el DOM de la página y no en una de sus entradas de datos**, como en el caso del XSS reflejado.
```
-Pendiente de estudiar un poco más-