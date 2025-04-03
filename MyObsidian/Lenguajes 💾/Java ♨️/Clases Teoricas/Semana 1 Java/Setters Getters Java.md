Los setters y getters son métodos especiales en Java que siguen el patrón de encapsulación para acceder y modificar variables privadas de una clase. Permiten controlar el acceso a los datos y aplicar validaciones.

## Getters

Los getters son métodos que permiten obtener el valor de una variable privada:

- Comienzan con el prefijo "get" seguido del nombre de la variable en formato camelCase
- Para variables booleanas, a menudo se usa el prefijo "is" en lugar de "get"
- Devuelven el tipo de datos de la variable que recuperan

```java
private String nombre;

// Getter para nombre
public String getNombre() {
    return nombre;
}

private boolean activo;

// Getter para variable booleana
public boolean isActivo() {
    return activo;
}
```

## Setters

Los setters son métodos que permiten modificar el valor de una variable privada:

- Comienzan con el prefijo "set" seguido del nombre de la variable en formato camelCase
- Generalmente tienen un parámetro del mismo tipo que la variable
- Normalmente son de tipo void (no devuelven valor)

```java
private String nombre;

// Setter para nombre
public void setNombre(String nombre) {
    this.nombre = nombre;
}

// Setter con validación
public void setEdad(int edad) {
    if (edad >= 0 && edad <= 120) {
        this.edad = edad;
    } else {
        throw new IllegalArgumentException("Edad inválida");
    }
}
```

## Beneficios

1. **Encapsulación**: Ocultan los detalles internos de implementación
2. **Validación**: Permiten validar datos antes de asignarlos
3. **Control de acceso**: Pueden hacer que propiedades sean de solo lectura (solo getter) o solo escritura (solo setter)
4. **Flexibilidad**: Permiten cambiar la implementación interna sin afectar el código que usa la clase

## Ejemplo completo

```java
public class Persona {
    private String nombre;
    private int edad;
    private boolean activo;
    
    // Constructor
    public Persona(String nombre, int edad) {
        this.nombre = nombre;
        this.edad = edad;
        this.activo = true;
    }
    
    // Getters
    public String getNombre() {
        return nombre;
    }
    
    public int getEdad() {
        return edad;
    }
    
    public boolean isActivo() {
        return activo;
    }
    
    // Setters
    public void setNombre(String nombre) {
        if (nombre != null && !nombre.trim().isEmpty()) {
            this.nombre = nombre;
        }
    }
    
    public void setEdad(int edad) {
        if (edad >= 0) {
            this.edad = edad;
        }
    }
    
    public void setActivo(boolean activo) {
        this.activo = activo;
    }
}
```

En la práctica, muchos IDE como Eclipse o IntelliJ IDEA pueden generar automáticamente estos métodos para ti.