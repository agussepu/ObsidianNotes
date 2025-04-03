En este caso explotaremos nuevamente las tracking id ([[Exploiting blind SQL injection by triggering conditional responses]]) y emplearemos caido para hacer fuerza bruta

```http
// En este caso vemos que con 1=1 se muestra el mensaje welcome y con 1=2 no se muestra siendo vulnerable
Cookie: TrackingId=gdFX0T2vTzlEi85Q' and 1=1--;
```

Con esta logica y ademas en este ejercicio sabemos que existe una tabla llamada users con columas username y password podemos verficar si el username de administrator comienza con a, si es verdad se muestra el welcome 


```http
// administrator comienza con la letra a es True
Cookie: TrackingId=gdFX0T2vTzlEi85Q' and ( select substring(username,1,1) from users where username='administrator' )='a'--;
```

Con esta logica podemos comenzar a fuzzear la data del contenido de password (una vez encontrada la primer letra nos movemos a la siguiente con subtring(password,2,1))

Para **automatizar** este fuzzing podemos usar el automate de Caido para introduccir un diccionario con la posible letras o podemos hacer un script de python

### Opción 1 Caido
1) cargamos el payload en automate
2) Vemos que debe haber uno que tenga un tamaño diferente a los demas significa que es verdadero(ya que ese muestra el mensaje de welcome)
![[Pasted image 20250328110509.png]]
3) Ya adivinamos el primer caracter (es un 2) y seguimos asi hasta encontrarlos todos

### Opción 2 Python

