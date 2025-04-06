### 🔹 **`interface` y `implements` en Java**

En Java, una **interfaz (`interface`)** es un contrato que define un conjunto de métodos que una clase debe implementar. Se usa para lograr **abstracción** y **herencia múltiple** (ya que Java no permite heredar de múltiples clases).

---

## 📌 **1. ¿Qué es una interfaz (`interface`)?**

Una interfaz es una colección de **métodos abstractos** (sin implementación) y **constantes**.

🔹 **Características**:

- No puede tener estado (variables de instancia).
    
- Solo puede contener **métodos abstractos** (antes de Java 8).
    
- Desde **Java 8**, puede tener **métodos por defecto (`default`)** y **métodos estáticos (`static`)** con implementación.
    
- No puede tener constructores.
    
- Se usa para definir **comportamientos comunes** entre clases no relacionadas.
    

---

## 📌 **2. ¿Cómo se define una interfaz?**

```java
interface Vehiculo {
    void acelerar(); // Método abstracto (sin implementación)
    void frenar();
}
```

---

## 📌 **3. ¿Qué hace `implements`?**

Una **clase** usa `implements` para proporcionar la implementación de los métodos de una interfaz.

```java
class Coche implements Vehiculo {
    @Override
    public void acelerar() {
        System.out.println("El coche está acelerando...");
    }

    @Override
    public void frenar() {
        System.out.println("El coche está frenando...");
    }
}
```

🔹 **Reglas importantes**:

- Una clase puede **implementar múltiples interfaces**.
    
- Debe proporcionar implementación a **todos** los métodos de la interfaz.
    

---

## 📌 **4. Implementación de múltiples interfaces**

Java permite que una clase implemente más de una interfaz, lo que simula **herencia múltiple**.

```java
interface Motor {
    void encender();
}

class Moto implements Vehiculo, Motor {
    @Override
    public void acelerar() {
        System.out.println("La moto acelera...");
    }

    @Override
    public void frenar() {
        System.out.println("La moto frena...");
    }

    @Override
    public void encender() {
        System.out.println("El motor de la moto se enciende...");
    }
}
```

---

## 📌 **5. Métodos `default` y `static` en interfaces (Java 8+)**

Desde Java 8, las interfaces pueden tener **métodos con implementación**.

```java
interface Computadora {
    void encender();

    default void apagar() { // Método con implementación
        System.out.println("Apagando la computadora...");
    }
}

class Laptop implements Computadora {
    @Override
    public void encender() {
        System.out.println("Encendiendo laptop...");
    }
}

public class Main {
    public static void main(String[] args) {
        Laptop miLaptop = new Laptop();
        miLaptop.encender(); // "Encendiendo laptop..."
        miLaptop.apagar(); // "Apagando la computadora..."
    }
}
```

🔹 **Ventajas de `default` y `static`**:

- Permiten agregar nuevos métodos sin afectar clases antiguas.
    
- Evitan duplicación de código.
    

---

## 📌 **6. Diferencia entre `abstract class` e `interface`**

|Característica|`abstract class`|`interface`|
|---|---|---|
|Métodos|Puede tener métodos con implementación y abstractos|Solo métodos abstractos (excepto `default` y `static` desde Java 8)|
|Herencia|Se extiende con `extends` (una sola clase)|Se implementa con `implements` (múltiples interfaces)|
|Variables|Puede tener atributos con estado|Solo constantes (`static final`)|
|Constructores|**Sí**, porque es una clase|**No**, porque no es una clase|

---

## 📌 **7. ¿Cuándo usar `interface` en vez de `abstract class`?**

- Usa **`interface`** cuando quieras **compartir comportamiento entre clases no relacionadas**.
    
- Usa **`abstract class`** cuando tengas una **jerarquía de clases con lógica compartida**.
    

---

## 📌 **8. Ejemplo real: Dispositivos electrónicos**

```java
interface Conectable {
    void encender();
    void apagar();
}

class Televisor implements Conectable {
    @Override
    public void encender() {
        System.out.println("Encendiendo televisor...");
    }

    @Override
    public void apagar() {
        System.out.println("Apagando televisor...");
    }
}

class Computadora implements Conectable {
    @Override
    public void encender() {
        System.out.println("Encendiendo computadora...");
    }

    @Override
    public void apagar() {
        System.out.println("Apagando computadora...");
    }
}

public class Main {
    public static void main(String[] args) {
        Conectable tv = new Televisor();
        Conectable pc = new Computadora();

        tv.encender();
        pc.apagar();
    }
}
```

✔ Esto permite tratar distintos dispositivos como **"Conectables"**, sin importar qué tipo sean.

---

### 🚀 **Conclusión**

✅ **`interface`**: Define un contrato de métodos que deben ser implementados.  
✅ **`implements`**: Permite que una clase implemente una o más interfaces.  
✅ **Ventajas**:

- Flexibilidad y **herencia múltiple**.
    
- Facilita el **polimorfismo**.
    
- Separa **qué hace un objeto** de **cómo lo hace**.
    
