1. Lo primero que debemos de hacer es *terminar de validar* con que token validan el usuario dentro de las cookies, en el ejemplo que estamos viendo suponemos que usaba la cookie ACCESS_TOKEN por lo que lo mas fácil para validar si se usa ese token para identificar al usuario es *borrar el token y ver que pasa* 

![[validacionTokenIDOR.png]]
	Como vemos eliminamos el ACCESS_TOKEN y *la validación sigue funcionando* por lo que no nos servirá la vulnerabilidad en el JWT ya que parece que no lo utiliza para validar el usuario actual. No significa que no se use en la aplicación pero no nos servirá en este mecanismo.
	***(+)*** Pero en este punto *podemos asegurar* que lo que se usa para identificar al usuario es la *auth cookie*

2. Intentaremos *reducir* los mas posible los *datos adicionales* dentro de la petición HTTP, en este ejemplo reduciendo valor nos damos cuenta que la sección de email siempre debe de estar sino devolvera un fallo por lo que lo *anotaríamos en nuestro punteros*. 
	La petición POST par actualizar los valores del usuario debe de incluir el Email parameter en el body  pero no parece validarlo a la hora de cambiar datos