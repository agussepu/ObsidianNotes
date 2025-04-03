---
aliases:
  - java main()
---
---
Excelente pregunta. Voy a explicarte cada parte de la declaración del método main:

```java
public static void main(String[] args)
```

1. **`public`**:
    
    - Significa que el método es accesible desde cualquier otra clase
    - La JVM (Java Virtual Machine) necesita poder ejecutar este método desde cualquier lugar
    - Sin `public`, la JVM no podría iniciar la ejecución del programa
2. **`static`**:
    
    - Permite que el método se ejecute sin crear un objeto de la clase
    - La JVM llama al main antes de crear cualquier instancia de la clase
    - Un método estático pertenece a la clase, no a un objeto específico
    - Permite ejecutar el método directamente desde la clase sin instanciarla
3. **`void`**:
    
    - Indica que el método no devuelve ningún valor
    - El método main es un punto de entrada, no necesita retornar nada
    - Simplemente inicia la ejecución del programa
4. **`String[] args`**:
    
    - Permite pasar argumentos desde la línea de comandos al programa
    - `args` es un arreglo de cadenas que contiene los argumentos
    - Útil para configurar o modificar el comportamiento del programa al iniciarlo

Ejemplo práctico:

```java
public class EjemploMain {
    // Método main con argumentos desde línea de comandos
    public static void main(String[] args) {
        // Imprimir número de argumentos
        System.out.println("Número de argumentos: " + args.length);
        
        // Imprimir cada argumento
        for (String arg : args) {
            System.out.println("Argumento: " + arg);
        }
    }
}
```

Si ejecutas: `java EjemploMain hola mundo` Imprimirá:

```
Número de argumentos: 2
Argumento: hola
Argumento: mundo
```

Es un estándar definido por Java para garantizar un punto de entrada único y consistente en todos los programas.