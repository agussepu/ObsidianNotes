**Funciones Lambda**

Las funciones lambda son también conocidas como funciones anónimas debido a que no se les asigna un nombre explícito al definirlas. Se utilizan para crear pequeñas funciones en el lugar donde se necesitan, generalmente para una operación específica y breve. En Python, una función lambda se define con la palabra clave ‘**lambda**‘, seguida de una lista de argumentos, dos puntos y la expresión que desea evaluar y devolver.

Una de las ventajas de las funciones lambda es su simplicidad sintáctica, lo que las hace ideal para su uso en operaciones que requieren una función por un breve momento y para casos donde la definición de una función tradicional completa sería excesivamente verbosa.

**Usos comunes de las Funciones Lambda**

- **Con funciones de orden superior**: Como aquellas que requieren otra función como argumento, por ejemplo, ‘**map()**‘, ‘**filter()**‘ y ‘**sorted()**‘.
- **Operaciones simples**: Para realizar cálculos o acciones rápidas donde una función completa sería innecesariamente larga.
- **Funcionalidad en línea**: Cuando se necesita una funcionalidad simple sin la necesidad de reutilizarla en otro lugar del código.

En esta clase, aprenderemos cómo y cuándo utilizar las funciones lambda de manera efectiva, además de entender cómo pueden ayudarnos a escribir código más limpio y eficiente. Aunque su utilidad es amplia, también discutiremos las limitaciones de las funciones lambda y cómo el abuso de estas puede llevar a un código menos legible.

Al dominar las funciones lambda, ampliarás tu conjunto de herramientas de programación en Python, permitiéndote escribir código más conciso y funcional.

```python
cuadrado =  lambda x: x**2
print(cuadrado(6))

cuadrado =  lambda x, y: x + y
print(cuadrado(6,5))

#map
numeros = [1, 2, 3, 4, 5]
cuadrados = list(map(lambda x: x**2, numeros)) #usamos el list ya que sino el map devuelve un objeto iterable
print(cuadrados)

#filter devuelve los mismp que map nada mas que devuelve en base a si la condicion de la funcion devuvle true o false 
numeros = [1, 2, 3, 4, 5]
cuadrados = list(filter(lambda x: x % 2 == 0, numeros))
print(cuadrados)
```