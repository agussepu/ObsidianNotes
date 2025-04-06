**JWTs** -> Json web tokens

Ya sabiendo que cookies son utilizadas para identificar al usuarios vemos que en este ejemplo que la cookie *ACCESS_TOKEN* parece ser un *JWT*    por lo que la analizaremos en el decodificador

***¡!*** Parece que el hecho que haya muchos `ey`  `.ey` puede ser indicativo de un JWT basado en la experiencia de rs0n, ademas parece que al haber un . casi al final y una breve secuencia de caracteres podria indicar que es una firma del JWT
![[JWT_IDOR.png]]

![[JWT_IDOR_Decode.png]]

Parece ser en este ejemplo que el `nameid` es un identificador, esto podria ser posiblemente un identificador secuencial ( lo que seria el escenario ideal a la hora de buscar un IDOR o por lo menos algun patron predecible para cambiar el user id) 

# Firma JWT ( Bypass )
El hecho de que sea un JWT nos impide poder cambiar de manera directa el user id ya que este contiene una firma la cual esta diseñada para garantizar la integridad del token. Por lo que primero tengo que bypasear cualquier mecanismo que valide dicha firma para yo poder cambiar ese token.

Para poder hacer **Bypass** a la firma...
1. Debemos saber que tipo de *cifrado* emplea la firma
2. Vemos si esta *validando* la firma antes de tomar el valor del user id (agregamos un caracter a la firma)
3. En caso de que no se estén validando probaremos *cambiar los user id* desde burp


**En este ejemplo**:
1. Veremos al seleccionar el contenido del token que emplea *HS256* este tipo de cifrado es simetrico ( Este tipo de cifrado no es comúnmente usado ya que NO es asimétrico, puede que no sea valioso el token o que no le pusieron énfasis a la seguridad )
![[BypassJWT.png]]
![[cifradoJWT_IDOR.png]]

2. Verificamos si valida la firma antes de tomar el user id agregando un caracter a la firma y como vemos nos devuelve un código de estado 200 por lo que no la valida antes (En este ejemplo *borra un caracter* en vez de agregar uno) ![[validaJW.png]]
3. Al no estar validada la firma probaremos cambiar los valores de user id para ver si podemos acceder a otra cuenta (*Recoda sacar los % sobrantes de la petición HTTP*)![[valoresJWT.png]]![[Pasted image 20250405222705.png]]
4. Guardaremos los JSON en las notas pertenecientes a cada cuenta para seguir con el bypass