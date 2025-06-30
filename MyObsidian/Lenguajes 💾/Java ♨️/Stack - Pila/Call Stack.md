### ¿Qué es el call stack?
Es una estructura de datos de tipo **LIFO** (Last In, First Out) que utiliza el sistema para llevar el control de las **funciones o métodos activos**. Cada vez que se llama a una función, se **empuja un nuevo marco de pila (stack frame)** con sus variables locales, parámetros y dirección de retorno. Cuando una función termina, se **saca (pop)** ese marco de la pila.

### Conceptos clave en Java:

- Cada llamada se apila en el call stack.
    
- Al completarse, se desapila y vuelve al punto de llamada anterior.
    
- Si se recurre mucho (por ejemplo, `solve(10000, ...)`), se puede producir una **`StackOverflowError`**.

Una de las ventajas de utilizar una pila para implementar la invocación de métodos es que permite a los programas utilizar la recursividad. Es decir, permite que un método se llame a sí mismo, como se discutió en el Capítulo 5. Hemos descrito implícitamente el concepto de pila de llamadas y el uso
de marcos dentro de nuestra representación de trazas de recursividad en ese capítulo. Curiosamente, los primeros lenguajes de programación, como Cobol y Fortran, no usaban originalmente pilas de llamadas para implementar llamadas a funciones y procedimientos. Pero debido a la elegancia y eficiencia que permite la recursividad, todos los lenguajes de programación modernos, incluyendo las versiones modernas de lenguajes clásicos como Cobol y Fortran, utilizan una pila en tiempo de ejecución para las llamadas a métodos y procedimientos.
