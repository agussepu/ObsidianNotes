En Java, `equals`, `equalsIgnoreCase`, `compareTo` y `==` se utilizan para comparar valores, pero cada uno tiene su propósito y funcionamiento específico:

---
### 1️⃣ `equals(Object obj)`

✔ **Uso:** Compara el contenido de dos objetos.  
✔ **Definido en:** `Object`, pero sobrescrito en `String`, `Integer`, `List`, etc.  
✔ **Ejemplo:**

```java
String s1 = "Hola";
String s2 = "Hola";
System.out.println(s1.equals(s2)); // true (compara contenido)
```

✔ **Importante:**

- Se usa para comparar objetos, no referencias.
    
- En `String`, compara caracteres, distinguiendo mayúsculas y minúsculas.

---

### 2️⃣ `equalsIgnoreCase(String str)`

✔ **Uso:** Compara dos cadenas sin diferenciar mayúsculas y minúsculas.  
✔ **Definido en:** `String`.  
✔ **Ejemplo:**

```java
String s1 = "Hola";
String s2 = "HOLA";
System.out.println(s1.equalsIgnoreCase(s2)); // true
```

---

### 3️⃣ `compareTo(String str)`

✔ **Uso:** Compara dos cadenas lexicográficamente (según el orden ASCII).  
✔ **Devuelve:**

- `0` si son iguales
    
- `< 0` si el primer string es menor
    
- `> 0` si el primer string es mayor  
    ✔ **Definido en:** `Comparable<T>` (implementado en `String`).  
    ✔ **Ejemplo:**

```java
String s1 = "Hola";
String s2 = "Mundo";
System.out.println(s1.compareTo(s2)); // Negativo (-5) porque 'H' < 'M'
```

✔ **Importante:**

- Útil para ordenar listas de strings.
    

---

### 4️⃣ `==` (Comparación de referencias)

✔ **Uso:** Compara si dos referencias apuntan al mismo objeto en memoria.  
✔ **Ejemplo:**

```java
String s1 = new String("Hola");
String s2 = new String("Hola");
System.out.println(s1 == s2); // false (diferentes objetos en memoria)
```

✔ **Importante:**

- En **tipos primitivos** (`int`, `char`, `double`, etc.), compara valores directamente.
    
- En **objetos**, compara referencias en memoria.
    
---

### ⚡ Diferencias clave:

| Método             | Compara                | Sensible a mayúsculas | Devuelve         |
| ------------------ | ---------------------- | --------------------- | ---------------- |
| `equals`           | Contenido del objeto   | Sí                    | `true` o `false` |
| `equalsIgnoreCase` | Contenido del String   | No                    | `true` o `false` |
| `compareTo`        | Orden lexicográfico    | Sí                    | `0`, `<0`, `>0`  |
| `==`               | Referencias en memoria | N/A                   | `true` o `false` |

Si necesitas verificar contenido, usa `equals`. Si comparas Strings sin importar mayúsculas, usa `equalsIgnoreCase`. Para ordenar cadenas, usa `compareTo`. Si comparas referencias, usa `==`.
