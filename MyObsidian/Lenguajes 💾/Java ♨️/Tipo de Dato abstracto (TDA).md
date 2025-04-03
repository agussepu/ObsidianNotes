Aquí tienes ejemplos de cómo podrías implementar una **clase abstracta** en Java para definir un **Tipo de Dato Abstracto (TDA)**, basado en la idea de `Racional`, pero permitiendo la extensibilidad a otros tipos de números fraccionarios.

---

### **Ejemplo: Clase abstracta `NumeroFraccionario`**

Esta clase define una estructura básica para números fraccionarios, pero no implementa los métodos de operaciones matemáticas, dejando que las clases concretas (como `Racional`) lo hagan.

```java
// Clase abstracta que define un tipo de dato abstracto (TDA)
public abstract class NumeroFraccionario {
    protected int numerador;
    protected int denominador;

    // Constructor
    public NumeroFraccionario(int numerador, int denominador) {
        if (denominador == 0) {
            throw new ArithmeticException("El denominador no puede ser cero");
        }
        this.numerador = numerador;
        this.denominador = denominador;
        simplificar();
    }

    // Método para calcular el máximo común divisor (MCD)
    protected int mcd(int a, int b) {
        while (b != 0) {
            int temp = b;
            b = a % b;
            a = temp;
        }
        return Math.abs(a);
    }

    // Método para simplificar la fracción
    protected void simplificar() {
        int mcd = mcd(numerador, denominador);
        numerador /= mcd;
        denominador /= mcd;
        if (denominador < 0) { 
            numerador = -numerador;
            denominador = -denominador;
        }
    }

    // Método abstracto: las clases hijas deben definir su comportamiento
    public abstract NumeroFraccionario sumar(NumeroFraccionario otro);
    public abstract NumeroFraccionario restar(NumeroFraccionario otro);
    public abstract NumeroFraccionario multiplicar(NumeroFraccionario otro);
    public abstract NumeroFraccionario dividir(NumeroFraccionario otro);

    // Método toString común para todas las subclases
    @Override
    public String toString() {
        return (denominador == 1) ? String.valueOf(numerador) : numerador + "/" + denominador;
    }
}
```

---

### **Ejemplo: Clase `Racional` que extiende `NumeroFraccionario`**

Ahora `Racional` hereda de `NumeroFraccionario` y proporciona implementaciones específicas para los métodos abstractos.

```java
// Clase concreta que hereda de NumeroFraccionario
public class Racional extends NumeroFraccionario {

    // Contador de instancias
    private static int cuenta = 0;

    // Constructor que usa el de la superclase
    public Racional(int numerador, int denominador) {
        super(numerador, denominador);
        cuenta++;
    }

    @Override
    public Racional sumar(NumeroFraccionario otro) {
        int num = this.numerador * otro.denominador + otro.numerador * this.denominador;
        int den = this.denominador * otro.denominador;
        return new Racional(num, den);
    }

    @Override
    public Racional restar(NumeroFraccionario otro) {
        int num = this.numerador * otro.denominador - otro.numerador * this.denominador;
        int den = this.denominador * otro.denominador;
        return new Racional(num, den);
    }

    @Override
    public Racional multiplicar(NumeroFraccionario otro) {
        return new Racional(this.numerador * otro.numerador, this.denominador * otro.denominador);
    }

    @Override
    public Racional dividir(NumeroFraccionario otro) {
        if (otro.numerador == 0) {
            throw new ArithmeticException("No se puede dividir por cero");
        }
        return new Racional(this.numerador * otro.denominador, this.denominador * otro.numerador);
    }

    public static int getCuenta() {
        return cuenta;
    }
}
```

---

### **¿Por qué usar una clase abstracta?**

1. **Reutilización de código**: La clase `NumeroFraccionario` define el comportamiento común para fracciones (métodos de simplificación, validación, etc.), evitando repetir código en `Racional`.
    
2. **Extensibilidad**: Si en el futuro necesitas otro tipo de fracción (por ejemplo, `FraccionMixta`), solo tendrías que crear una nueva subclase en lugar de modificar `Racional`.
    
3. **Encapsulación y Abstracción**: La clase abstracta oculta detalles de implementación y solo expone los métodos que deben ser implementados.
    

---

### **Ejemplo de uso**

```java
public class Main {
    public static void main(String[] args) {
        Racional r1 = new Racional(3, 4);
        Racional r2 = new Racional(2, 5);

        Racional suma = r1.sumar(r2);
        System.out.println("Suma: " + suma);

        Racional resta = r1.restar(r2);
        System.out.println("Resta: " + resta);

        Racional producto = r1.multiplicar(r2);
        System.out.println("Producto: " + producto);

        Racional division = r1.dividir(r2);
        System.out.println("División: " + division);

        System.out.println("Total de objetos creados: " + Racional.getCuenta());
    }
}
```

---
## ¿Para qué sirve que la clase sea abstracta?
Hacer que una clase sea **abstracta** en Java tiene varias ventajas:

1. **Obligar a la implementación de ciertos métodos**: Si declaras métodos abstractos en una clase base, cualquier subclase está obligada a proporcionar una implementación, garantizando un comportamiento uniforme.
    
2. **Evitar la instanciación directa**: No puedes crear instancias de una clase abstracta, lo que tiene sentido si la clase representa una entidad general y debe ser extendida por clases concretas.
    
3. **Facilitar la reutilización y extensibilidad**: La clase abstracta puede proporcionar métodos comunes (como `simplificar()`) y definir la estructura de comportamiento sin imponer detalles de implementación.