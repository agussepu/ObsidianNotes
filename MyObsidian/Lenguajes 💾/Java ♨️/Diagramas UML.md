---
aliases:
---
---
# 📌 Notación UML

![[Pasted image 20250401123822.png]]

---

📌 **Indicaciones UML**:

1. **Encapsulación**: Los atributos son `private (-)`, y los métodos `public (+)`.
    
2. **Herencia**: Se representa con una flecha vacía desde la subclase a la superclase.
    
3. **Métodos y atributos**: Se especifican con su tipo (`String`, `double`, `int`, etc.).
    
4. **Clases**: Se encierran en cuadros con sus tres secciones (nombre, atributos y métodos).

5. **Abstracto**: Indica que el elemento es abstracto 

---
# Flechas en UML 

#### **1. Flecha con cabeza vacía y línea continua (Herencia - Generalización)**

📌 **Uso:** Representa que una clase hereda de otra (relación _es un_).

🔹 **Ejemplo:** `EmpleadoAsalariado` hereda de `Empleado`.

```
Empleado  ◁────── EmpleadoAsalariado
```

En UML:

- La flecha apunta hacia la **superclase** (`Empleado`).
    
- `EmpleadoAsalariado` es una **subclase** (especialización de `Empleado`).
    

#### **2. Flecha con cabeza vacía y línea discontinua (Implementación de una interfaz)**

📌 **Uso:** Representa que una clase implementa una **interfaz**.

🔹 **Ejemplo:** Si `Empleado` fuera una interfaz y `EmpleadoAsalariado` la implementara:

```
Empleado ◁⋅⋅⋅⋅⋅ EmpleadoAsalariado
```

En UML:

- `Empleado` sería una **interfaz**.
    
- `EmpleadoAsalariado` implementa `Empleado`.
    

#### **3. Flecha con cabeza llena y línea continua (Composición)**

📌 **Uso:** Representa una relación **fuerte** (una clase contiene otra y si la clase contenedora se destruye, también lo hace la contenida).

🔹 **Ejemplo:** `Factura` contiene una lista de `Item`.

```
Factura ◆────── Item
```

En UML:

- `Factura` **posee** `Item` (si `Factura` se elimina, los `Item` también).
    

#### **4. Flecha con cabeza vacía y línea continua (Agregación)**

📌 **Uso:** Relación **débil** entre clases (una clase usa otra, pero no la posee).

🔹 **Ejemplo:** Un `Departamento` tiene una lista de `Empleado`, pero los empleados pueden existir sin el departamento.

```
Departamento ◇────── Empleado
```

En UML:

- `Departamento` tiene empleados, pero si se borra el `Departamento`, los `Empleado` pueden seguir existiendo.
    

---

### **Texto sobre las flechas (Roles y multiplicidad)**

📌 **Uso:** Explica cómo se relacionan las clases.

🔹 **Ejemplo:** Un `Departamento` tiene múltiples `Empleado` (1 a muchos).

```
Departamento ◇────── Empleado
       1             0..*
```

- `1` → Un solo `Departamento`.
    
- `0..*` → Puede haber **cero o más** `Empleado`.
    

---

### **Aplicación en tu código**

Para representar tu código en UML:

```
            ◁────── EmpleadoAsalariado
            ◁────── EmpleadoPorHora
Empleado ◁────── EmpleadoPorComision ◁────── EmpleadoBaseMasComision
```

Si necesitas un diagrama gráfico, dime y te lo genero. 🚀