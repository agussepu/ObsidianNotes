```python
lista_numeros = [12, 23, 45, 553, 67]

print(lista_numeros)

# Agrega un elemento a la lista
lista_numeros.append(20)
lista_numeros += [30]

# Agrega un conjunto de nuemros
lista_numeros.extend([13,14])

# Ordena elementos de la lista de menor a mayor
lista_numeros = sorted(lista_numeros)

# Elimina un elemento de la lista
del lista_numeros[0] #elimina el del indice 0

print(lista_numeros[2:3])

# Inserta en un lugar de la lista un elemento
lista_numeros.insert(1,9)

# Eliminar el ultimo elemento de la lista
lista_numeros.pop()

# Conocer el indice de un elemento
print(lista_numeros.index(9))

# con set podemos limpiar lo repetido y luego volver a hacerlo lista
lista_numeros = list(set(lista_numeros))

#con min y max podemos obtener el valor mas grande y maas chico de una lista
# y con len el tamaño de la lista ademas con sum podemos sumar todos los valores de una lista
# y para redondear un numero usamos round
```