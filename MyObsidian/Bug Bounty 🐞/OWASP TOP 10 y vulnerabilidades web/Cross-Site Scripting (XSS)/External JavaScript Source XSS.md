---
tags:
  - HackingTools
---
---
# Robo de Cookie de sesión
Tengamos en cuenta que este tipo de ataque no puede darse si el navegador tiene activado el **HttpOnly** 
![[Pasted image 20250111183032.png]]

Las HttpOnly Cookies son un tipo especial de cookie que se diferencia por su nivel de seguridad. **Estas cookies están diseñadas para ser inaccesibles desde el lado del cliente**, es decir, desde el navegador web del usuario. Esto significa que no se pueden manipular ni acceder mediante _scripts_ del lado del cliente, como JavaScript. Es decir, solo pueden ser gestionadas por el servidor web. https://keepcoding.io/blog/que-es-y-como-funciona-httponly-cookies/

---
En caso de poder injectar comandos haremos ejecutar un documento remoto de nuestro equipo ![[Pasted image 20250111183622.png]]
Dicho documento sera un archivo javascript:
![[Pasted image 20250111183721.png]]

De manera que poniendonos en escucha con python recibiremos la cookie del usuario en cuestion.
![[Pasted image 20250111183910.png]]

De manera que ahora podemos usar esa cookie en nuestro navegador de manera que estaremos logeados como el usuario al que le pertenezca esa cookie
![[Pasted image 20250111184052.png]]

---
#  CSRF_TOKEN
Con XSS hacemos lo siguiente en la pagina web o servidor para que ejecute el archivo que tenemos en local
![[Pasted image 20250113144618.png]]
Montamos en local el archivo javascript para recibir el token
![[Pasted image 20250113150007.png]]

![[Pasted image 20250113150141.png]]

