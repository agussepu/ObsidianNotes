---
aliases:
  - OpTernario
---
## Operador ternario 
```java
condición ? valor_si_verdadero : valor_si_falso

return (denominador == 1) ? String.valueOf(numerador) : numerador + "/" + denominador;

```
- Si `denominador == 1`, devuelve solo el `numerador` como `String`.
    
- Si `denominador` es distinto de `1`, devuelve la fracción `"numerador/denominador"`.


2️⃣ **Ejemplos de salida:**

```java
`Racional r1 = new Racional(3, 1); System.out.println(r1.toString()); // 3

Racional r2 = new Racional(3, 4); System.out.println(r2.toString()); // 3/4
```