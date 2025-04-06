hasta este momento del ejemplo únicamente hemos encontrado el objeto de user del cual tenemos los parámetros en la petición HTTP

![[userObject_IDOR.png]]
En este punto se investiga sobre el mecanismo de payment el cual parece que hace peticiones a una API y ademas en este mecanismo a la hora de sacar el *ACCESS_TOKEN* devuelve un error por lo que parece que *aca si se usa ese token* y como habíamos visto anteriormente este token *utilizaba una encryption simétrica con HS256*

*Pero* como vemos aca a la hora de remover un caracter al JWT devuelve un error por lo que ahora parece que *si esta validando* la firma de dicho token
![[paymentIDOR.png]]