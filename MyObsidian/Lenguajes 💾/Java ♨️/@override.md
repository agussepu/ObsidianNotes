---
aliases:
  - JavaObject
---

# ¿Para qué se emplea `@Override` en el código

`@Override` indica que un método está **sobrescribiendo** uno de la superclase (`Object`).  

```java
@Override
public String toString() {
    return (denominador == 1) ? String.valueOf(numerador) : numerador + "/" + denominador;
}
```

Esto sobrescribe el método `toString()` de `Object`, permitiendo que cuando imprimas un `Racional`, se muestre como `"a/b"` en lugar de la representación por defecto de `Object`.

```java
Racional r = new Racional(3, 4);
System.out.println(r);  // Muestra "3/4"
```

✔ Si no usáramos `@Override`, Java **no obligaría** a seguir la firma correcta del método original, lo que podría causar errores.

`@Override` se usa para sobrescribir métodos de `Object` (como `toString()`) y evitar errores de firma.


----
### **1) ¿Qué es una superclase en Java?**

Una **superclase** es una clase de la cual otra clase **hereda atributos y métodos**.

Cuando una clase hereda de otra, la clase que hereda se llama **subclase**, y la clase de la cual hereda se llama **superclase**.

#### **Ejemplo de superclase y subclase**

```java
// Superclase
class Animal {
    void hacerSonido() {
        System.out.println("Haciendo un sonido...");
    }
}

// Subclase (hereda de Animal)
class Perro extends Animal {
    void ladrar() {
        System.out.println("Guau guau!");
    }
}

public class Main {
    public static void main(String[] args) {
        Perro miPerro = new Perro();
        miPerro.hacerSonido(); // Llamado al método heredado de Animal
        miPerro.ladrar();      // Método propio de Perro
    }
}
```

📌 **Explicación:**

- `Animal` es la **superclase** porque `Perro` hereda de ella.
    
- `Perro` es la **subclase**.
    
- `Perro` puede usar el método `hacerSonido()` porque lo hereda de `Animal`.
    

---

### **2) ¿Qué es `Object` en Java?**

`Object` es la **superclase base de todas las clases en Java**.  
Si una clase no hereda explícitamente de otra, hereda **implícitamente** de `Object`.

```java
class MiClase {
    // Esta clase hereda implícitamente de Object
}
```

📌 Esto significa que **todas** las clases tienen acceso a los métodos definidos en `Object`.

---

### 3) Métodos de la clase `Object`

La clase `Object` tiene métodos básicos que pueden ser sobrescritos (`@Override`) en nuestras clases personalizadas.

Algunos métodos importantes de `Object`:

| Método               | Descripción                                         |
| -------------------- | --------------------------------------------------- |
| `toString()`         | Devuelve una representación en texto del objeto.    |
| `equals(Object obj)` | Compara si dos objetos son iguales.                 |
| `hashCode()`         | Retorna un código hash del objeto.                  |
| `getClass()`         | Retorna la clase del objeto en tiempo de ejecución. |
| `clone()`            | Crea una copia del objeto (si es `Cloneable`).      |
### **Conclusión**
✅ Una **superclase** es la clase de la cual otra clase hereda.  
✅ `Object` es la **superclase base** de **todas** las clases en Java.  
✅ Sus métodos (`toString()`, `equals()`, `hashCode()`, etc.) pueden ser sobrescritos con `@Override`.