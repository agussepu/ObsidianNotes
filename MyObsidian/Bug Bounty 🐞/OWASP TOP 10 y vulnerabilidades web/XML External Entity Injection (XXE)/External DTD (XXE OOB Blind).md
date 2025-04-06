---
tags:
  - HackingTools
---
---
En caso de ejecutar el XEE y que no sea vea nada en el output (similar a la XEE pero a ciegas) o en caso que la web no permita inyectar entidades dentro los formularios XML (&myFile) en dicho caso podemos dejar en este caso el mail sin modificar pero en el DTD hacemos lo siguiente
![[Pasted image 20250114134428.png]]
De manera que hacemos una peticion a nuestro equipo local y de esa manera ejecutar un script, por lo que debemos con python montar un servidor por el puerto 80 para recibir la peticion. Dicho archivo a ejecutar `malicious.dtd` consta de lo siguiente:
![[Pasted image 20250114135749.png]]

---
## Automatización del proceso
![[Pasted image 20250114164518.png]]