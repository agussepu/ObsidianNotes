	## Clases
Una clase es una plantilla o un plano que define la estructura y el comportamiento que tendrán los objetos creados a partir de ella. Define:
- Atributos (variables)
- Comportamientos (métodos)
- Constructores
- Otras características
```java
public class Coche {
    // Variables de instancia
    private String marca;
    private String modelo;
    private int año;
    
    // Constructor
    public Coche(String marca, String modelo, int año) {
        this.marca = marca;
        this.modelo = modelo;
        this.año = año;
    }
    
    // Métodos
    public void arrancar() {
        System.out.println("El coche está arrancando");
    }
    
    public void frenar() {
        System.out.println("El coche está frenando");
    }
}
```

## Objetos
Un objeto es una instancia de una clase. Cuando creas un objeto, estás creando una entidad concreta basada en la plantilla de la clase. Cada objeto:
- Tiene su propio estado (valores de sus variables)
- Puede realizar acciones (invocar métodos)
- Ocupa espacio en memoria
```java
// Crear objetos de la clase Coche
Coche miCoche = new Coche("Toyota", "Corolla", 2023);
Coche otroCoche = new Coche("Honda", "Civic", 2022);

// Usar los objetos invocando sus métodos
miCoche.arrancar();
otroCoche.frenar();
```

## Métodos
Los métodos son funciones definidas dentro de una clase que describen el comportamiento de los objetos. Pueden:
- Manipular datos (variables)
- Realizar cálculos
- Ejecutar acciones
- Devolver valores
```java
tipoDeRetorno nombreDelMetodo(parámetros) {
    // Cuerpo del método
    return valor; // Si el tipo de retorno no es void
}
```

## Variables de instancia
Las variables de instancia (también llamadas atributos o campos) son variables definidas a nivel de clase que:
- Almacenan el estado de cada objeto
- Cada objeto tiene su propia copia de estas variables
- Sus valores pueden ser diferentes para cada instancia
- Normalmente se declaran como private para encapsulación