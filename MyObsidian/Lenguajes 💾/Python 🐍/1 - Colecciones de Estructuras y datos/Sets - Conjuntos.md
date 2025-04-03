Los conjuntos son una colección de elementos sin orden y sin elementos repetidos, inspirados en la teoría de conjuntos de las matemáticas. Son ideales para la gestión de colecciones de elementos únicos y operaciones que requieren eliminar duplicados o realizar comparaciones de conjuntos.

```python
miConjunto = {1, 2, 3}
segundoConjunto = {1, 2, 3, 4, 5}

# Añade elementos al conjunto
miConjunto.add(4)

# Elimina elementos del conjunto
miConjunto.remove(1)

miConjunto.discard(1)

# Añade varios elementos
miConjunto.update({26,8,1})

# interseccion, ademas se puede usar uniones y diferencias
conjunto_interseccion = miConjunto.intersection(segundoConjunto)

# Verifica y devulve true o false si es un subconjunto
print(miConjunto.issubset(segundoConjunto))

# Verificar si un numero esta en mi conjunto
print(3 in miConjunto)
```


**Características de los Conjuntos**

- **Unicidad**: Los conjuntos automáticamente descartan elementos duplicados, lo que los hace perfectos para recolectar elementos únicos.
- **Desordenados**: A diferencia de las listas y las tuplas, los conjuntos no mantienen los elementos en ningún orden específico.
- **Mutabilidad**: Los elementos de un conjunto pueden ser agregados o eliminados, pero los elementos mismos deben ser inmutables (por ejemplo, no puedes tener un conjunto de listas, ya que las listas se pueden modificar).

**Operaciones con Conjuntos**

Exploraremos las operaciones básicas de conjuntos que Python facilita, como:

- **Adición y Eliminación**: Añadir elementos con ‘**add()**‘ y eliminar elementos con ‘**remove()**‘ o ‘**discard()**‘.
- **Operaciones de Conjuntos**: Realizar uniones, intersecciones, diferencias y diferencias simétricas utilizando métodos o operadores respectivos.
- **Pruebas de Pertenencia**: Comprobar rápidamente si un elemento es miembro de un conjunto.
- **Inmutabilidad Opcional**: Usar el tipo ‘**frozenset**‘ para crear conjuntos que no se pueden modificar después de su creación.

**Uso de Conjuntos en Python**

- **Eliminación de Duplicados**: Son útiles cuando necesitas asegurarte de que una colección no tenga elementos repetidos.
- **Relaciones entre Colecciones**: Facilitan la comprensión y el manejo de relaciones matemáticas entre colecciones, como subconjuntos y superconjuntos.
- **Rendimiento de Búsqueda**: Proporcionan una búsqueda de elementos más rápida que las listas o las tuplas, lo que es útil para grandes volúmenes de datos. 