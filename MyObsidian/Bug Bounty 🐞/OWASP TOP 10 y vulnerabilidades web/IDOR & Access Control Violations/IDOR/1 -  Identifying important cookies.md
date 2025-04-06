Usaremos el inspect del navegador para revisar las cookies, específicamente queremos ver cuales son *sessions tokens* y de esos cuales tienen el *HttpOnly* activado 
![[CookiesIdor.png]]

La flag **HttpOnly** en general se coloca en cualquier tipo cookie valiosa que los devs no quieran que atacantes tengas acceso.

Ahora lo que buscaremos son esas cookies que vimos que son necesarias para que el servidor identifique nuestro usuario y chequearemos que tengan la flag HttpOnly activada. En este caso se usa un cookie auth y no tiene la flag activa (esto lo anotariamos en la seccion de punteros)

![[httponlyIDOR.png]]


