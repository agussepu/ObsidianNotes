Las propiedades son un caso especial de decoradores que permiten a los desarrolladores añadir “**getter**“, “**setter**” y “**deleter**” a los atributos de una clase de manera elegante, controlando así el acceso y la modificación de los datos. En Python, esto se logra con el decorador ‘**@property**‘, que transforma un método para acceder a un atributo como si fuera un atributo público.

**Getters y Setters**

- El “**getter**” obtiene el valor de un atributo manteniendo el encapsulamiento y permitiendo que se ejecute una lógica adicional durante el acceso.
- El “**setter**” establece el valor de un atributo y puede incluir validación o procesamiento antes de que el cambio se refleje en el estado interno del objeto.
- El “**deleter**” puede ser utilizado para definir un comportamiento cuando un atributo es eliminado con del.

![[Pasted image 20250115171552.png]]