En caso de existir la posibilidad de un XSS en un formulario de un foro por ejemplo podemos verificarlo con etiquetas html en caso que funcionen podemos intentar meter una etiqueta `<script></script>`

![[Pasted image 20250111180500.png]]

Esto es un script simple que crea un formulario de mail y contraseña de manera que se tramitara por GET una petición con los datos introducidos y nos ponemos en escucha con `python -m http.server 80` recibiendo todas las peticiones que se tramiten por GET a nuestro equipo

También podemos redirigir al usuario a otra pagina. Aquí la posibilidad de clonar una web

![[Pasted image 20250111181918.png]]