Lo primero que debemos hacer es ver como la *web identifica* al usuario, y debemos ademas saber si la validación se hace en el *frontend* por ejemplo con react haciendo llamadas a la API o en el *backend*.

- ***¿Validación en el Frontend o Backend?*** Si al a la hora de ver el trafico por burpsuite (GET) vemos que en el response de la web *se encuentra nuestro nombre* de usuario probablemente la validación se de en el *backend* y si *no esta el nombre de usuario* en el response probablemente se de la validación en en el *frontend* con llamadas a la API
- ***Solicitud HTTP lo mas pequeña posible:***  Debemos de ir reduciendo la petición HTTP hasta quedarnos solamente con las partes que sirven para que identifique que usuario somos, por lo que a medida que vamos haciendo la petición mas chica vamos viendo si sigue respondiendo con un código de estado 200 (*quitamos las cookies que no sirven para identificar al usuario*)

