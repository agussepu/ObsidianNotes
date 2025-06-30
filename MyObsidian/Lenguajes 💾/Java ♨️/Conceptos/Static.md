---
aliases:
  - static
---

### 1) ¿Para qué sirve `static` en métodos y variables?

En Java, `static` se usa para indicar que un atributo o método pertenece a la **clase** en lugar de a las instancias individuales.

- **Variables `static` (atributos estáticos)**  
    Una variable `static` se comparte entre todas las instancias de la clase.  
    En el código, usamos:
    
    ```java
    private static int cuenta = 0;
    ```
    
    Esto significa que **todas** las instancias de `Racional` comparten la misma variable `cuenta`, que registra cuántos objetos se han creado.
    
- **Métodos `static`**  
    Un método `static` pertenece a la clase y no a los objetos.  
    En el código, tenemos:
    
    ```java
    public static int getCuenta() {
        return cuenta;
    }
    ```
    
    Este método permite acceder a `cuenta` sin necesidad de crear un objeto `Racional`:
    
    ```java
    System.out.println(Racional.getCuenta());
    ```
    

---

### **2) ¿Para qué sirve este constructor por defecto?**

```java
public Racional() {
    this(0, 1);
}
```

Este constructor **por defecto** permite crear un objeto `Racional` sin pasar argumentos.  
Es decir, al hacer:

```java
Racional r = new Racional();
```

Se llamará internamente al constructor:

```java
public Racional(int numerador, int denominador) {
    this.numerador = numerador;
    this.denominador = denominador;
    simplificar();
    cuenta++;
}
```

Por lo que `r` será **0/1**, que representa el número 0 en formato racional.

✔ Se usa `this(0, 1);` para reutilizar el constructor principal en lugar de repetir código.

---
### Resumen

1️⃣ `static` permite que un atributo o método pertenezca a la **clase** en lugar de a cada objeto.  
2️⃣ El constructor `Racional()` sin parámetros facilita la creación de un racional **0/1**.  