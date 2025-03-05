En caso de estar analizando una pagina y buscando archivos php existe la posibilidad de encontrar alguno que sea critico pero que a la hora de ejecutarlo por la web no veamos nada debido a que la misma este ejecutando dicho código de manera que solo vemos la ejecución. En este caso usaremos de ejemplo un archivo secret.php donde mediante un wrapper podemos codificar dicho contenido en base 64 para de manera local decodificarlo y ver el contenido del mismo. Esto desde el código fuente
![[Pasted image 20250115203901.png]]

Otra opción es rotar el contenido del archivo php para que no pueda ser interpretado y posteriormente en local podemos volver a rotar ese contenido de manera inversa para ver el contenido del mismo
![[Pasted image 20250115204126.png]]
![[Pasted image 20250115204242.png]]

Otra opcion es cambiar el utf para que no lo interprete
![[Pasted image 20250115204421.png]]

---
Existen wrappers que nos permiten ejecutar comandos a nivel de sistema LFI, estaremos usando burpsuite para esto.

Este primero nos permite de manera directa ejecutar comandos:
![[Pasted image 20250115204852.png]]

En el segundo cambiaremos la peticion de GET a POST de manera que podemos pasarle datos
![[Pasted image 20250115205347.png]]

En el tercero usaremos base 64 con un wrapper de manera que codificaremos un comando ![[Pasted image 20250115205739.png]]
De manera que mediante el siguiente wrapper podremos ejecutar comandos luego de cmd (recordar hacer ctrl + r en el hash de base 64)
![[Pasted image 20250115205855.png]]

Por ultimo php tiene algo extraño que si tenemos alguna cadena la que sea codificada en base 64 podemos mediante un wrapper decodificarla en base64 y volverla a codificar de manera que quedaria de nuevo codificada en base 64, pero existen manera de en medio de eso codificar en otros formatos las cadena y por alguna razon se agregaran caracteres (aca agrega la C a la cadena original) por lo que podemos agregar cualquier caracter que queramos.
![[Pasted image 20250115222814.png]]
Al introducir la cadena hay que tener en cuenta que debe ser al reves ![[Pasted image 20250115223056.png]]
Hay una herramienta que automatiza el hecho de buscar la codificacion para cada caracter que queremos agregar: https://github.com/synacktiv/php_filter_chain_generator
![[Pasted image 20250115223350.png]]
De manera que le pasamos la cadena y nos pasara el encode que la representa  
![[Pasted image 20250115230458.png]]

Por lo tanto mediante esta teoria podemos obtener una bash, primer ejecutanto comandos de manera mas sencilla con una cmd![[Pasted image 20250115230735.png]]
Aca van los comandos y ahi luego enviar una bash a nuestro equipo poniendonos en escucha con nc
![[Pasted image 20250115231020.png]]
![[Pasted image 20250115231220.png]]
![[Pasted image 20250115231250.png]]

