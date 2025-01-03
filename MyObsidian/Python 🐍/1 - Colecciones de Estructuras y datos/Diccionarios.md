Los diccionarios en Python son colecciones desordenadas de pares clave-valor. A diferencia de las secuencias, que se indexan mediante un rango numérico, los diccionarios se indexan con claves únicas, que pueden ser cualquier tipo inmutable, como cadenas o números.

**Características de los Diccionarios**

- **Desordenados**: Los elementos en un diccionario no están ordenados y no se accede a ellos mediante un índice numérico, sino a través de claves únicas.
- **Dinámicos**: Se pueden agregar, modificar y eliminar pares clave-valor.
- **Claves Únicas**: Cada clave en un diccionario es única, lo que previene duplicaciones y sobrescrituras accidentales.
- **Valores Accesibles**: Los valores no necesitan ser únicos y pueden ser de cualquier tipo de dato.

**Operaciones con Diccionarios**

- ### 1. **Crear un Diccionario**

Un diccionario se define con `{clave: valor}`
```python
`# Crear un diccionario simple 
inventario = {     "manzanas": (1.5, 10),  # Precio: 1.5, Cantidad: 10     "bananas": (2.0, 20),     "naranjas": (1.8, 15) } print(inventario)`
```
---

### 2. **Agregar un Elemento**
Puedes agregar una nueva clave-valor simplemente asignando:
```python
`# Agregar un producto nuevo 
inventario["uvas"] = (2.5, 8) print(inventario)`
```
---
### 3. **Actualizar un Valor**
Para modificar un valor, accede con la clave:
```python
# Actualizar el precio y la cantidad de un producto existente
inventario["manzanas"] = (1.6, 12) print(inventario)`
```
---
### 4. **Eliminar un Elemento**
Usa `del` o el método `pop`:
```python
# Actualizar el precio y la cantidad de un producto existente 
inventario["manzanas"] = (1.6, 12) print(inventario)`

# Usando del 
del inventario["bananas"] print(inventario)  
# Usando pop (te devuelve el valor eliminado) 
valor_eliminado = inventario.pop("naranjas") print(inventario) print("Elemento eliminado:", valor_eliminado)`
```
---
### 5. **Acceder a un Elemento**
Para acceder a un valor, usa su clave:
```python
`# Acceder a un elemento precio_manzanas, cantidad_manzanas = inventario["manzanas"] print("Precio de manzanas:", precio_manzanas) print("Cantidad de manzanas:", cantidad_manzanas)`
```
Maneja claves inexistentes con `get`:
```python
# Intentar acceder a un producto que no existe 
precio_uvas = inventario.get("uvas", "No encontrado") print(precio_uvas)`
```
---
### 6. **Recorrer un Diccionario**
Recorre las claves, valores o ambos:
```python
# Solo claves 
for producto in inventario:     
	print("Producto:", producto)  

# Claves y valores 
for producto, (precio, cantidad) in inventario.items():     
	print(f"{producto} - Precio: {precio}, Cantidad: {cantidad}")`
```
---
### 7. **Buscar en un Diccionario**
Verifica si una clave existe:
```python
# Buscar si un producto está en el inventario 
if "manzanas" in inventario:     
	print("Las manzanas están en el inventario.") 
else:     
	print("No hay manzanas.")`
```
---

### 8. **Ordenar un Diccionario**
Los diccionarios no tienen orden nativo, pero puedes usar `sorted`:
```python
`# Ordenar las claves del diccionario 
for producto in sorted(inventario.keys()): 
	print(producto, ":", inventario[producto])`
```
---

### 9. **Copiar un Diccionario**
Para copiarlo sin afectar el original:
```python
`# Crear una copia del diccionario copia_inventario = inventario.copy() copia_inventario["manzanas"] = (1.2, 5)  # Modificar la copia print("Original:", inventario) print("Copia:", copia_inventario)`
```
---

### 10. **Combinar Diccionarios**
Usa el operador `|` (Python 3.9+):
```python
`# Combinar dos diccionarios otro_inventario = {"kiwis": (3.0, 5), "mangos": (2.8, 7)} inventario_actualizado = inventario | otro_inventario print(inventario_actualizado)`
```
---

### Ejemplo Completo: Sistema Básico de Inventario
```python
`inventario = {     "manzanas": (1.5, 10),     "bananas": (2.0, 20),     "naranjas": (1.8, 15) }  # Agregar un nuevo producto inventario["uvas"] = (2.5, 8)  # Actualizar el precio y la cantidad de un producto existente inventario["manzanas"] = (1.6, 12)  # Mostrar todos los productos for producto, (precio, cantidad) in inventario.items():     print(f"{producto} - Precio: {precio}, Cantidad: {cantidad}")  # Eliminar un producto inventario.pop("bananas", None) print("\nInventario actualizado:", inventario)`
```