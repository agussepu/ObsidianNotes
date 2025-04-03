Los **arreglos polimórficos** en Java son arreglos que almacenan objetos de diferentes clases que comparten una relación de herencia. Esto es posible gracias al **polimorfismo**, un concepto de la programación orientada a objetos que permite tratar objetos de distintas subclases como si fueran de una clase base común.

### 🔹 **Características de los arreglos polimórficos en Java:**

1. **El arreglo se declara con el tipo de la superclase**
    
    - Se pueden almacenar instancias de cualquier subclase de esa superclase.
        
2. **Se pueden usar métodos de la superclase o sobrescritos en la subclase**
    
    - Si un método es sobrescrito en la subclase, se ejecutará la versión de la subclase.
        
3. **Facilita la programación genérica y la reutilización de código**
    
    - Se puede recorrer el arreglo sin importar la subclase específica de cada objeto.
        

---

### 🔹 **Ejemplo de arreglo polimórfico en Java**

Supongamos que tenemos una clase base `Animal` y dos subclases `Perro` y `Gato`:

```java
// Superclase
class Animal {
    public void hacerSonido() {
        System.out.println("Sonido genérico de animal");
    }
}

// Subclases
class Perro extends Animal {
    @Override
    public void hacerSonido() {
        System.out.println("Guau Guau!");
    }
}

class Gato extends Animal {
    @Override
    public void hacerSonido() {
        System.out.println("Miau Miau!");
    }
}

public class Main {
    public static void main(String[] args) {
        // Arreglo polimórfico
        Animal[] animales = new Animal[3];

        // Asignamos diferentes subclases al arreglo
        animales[0] = new Perro();
        animales[1] = new Gato();
        animales[2] = new Perro();

        // Recorremos el arreglo y llamamos al método polimórfico
        for (Animal a : animales) {
            a.hacerSonido(); // Se ejecuta el método correspondiente a cada subclase
        }
    }
}
```

### 🔹 **Salida del programa:**

```
Guau Guau!
Miau Miau!
Guau Guau!
```

---

### 🔹 **Beneficios de los arreglos polimórficos**

✅ **Flexibilidad:** Se pueden almacenar múltiples tipos de objetos sin cambiar la estructura del arreglo.  
✅ **Extensibilidad:** Si agregamos nuevas subclases, el código seguirá funcionando sin modificaciones.  
✅ **Uso de métodos comunes:** Se pueden llamar métodos de la superclase sin preocuparse de qué tipo de objeto específico es.
