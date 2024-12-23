**Funciones**

Las funciones son bloques de código reutilizables diseñados para realizar una tarea específica. En Python, se definen usando la palabra clave ‘**def**‘ seguida de un nombre descriptivo, paréntesis que pueden contener parámetros y dos puntos. Los parámetros son “**variables de entrada**” que pueden cambiar cada vez que se llama a la función. Esto permite a las funciones operar con diferentes datos y producir resultados correspondientes.

Las funciones pueden devolver valores al programa principal o a otras funciones mediante la palabra clave ‘**return**‘. Esto las hace increíblemente versátiles, ya que pueden procesar datos y luego pasar esos datos modificados a otras partes del programa.

```python
def saludo(nombre):
	print("hola " + nombre)
saludo(pepito)

# Cambiar varible global en local 
variable = "holaa"

def miFuncion():
	global varible
	variable = "Soy global y fui modificado"
print(variable)
```

**Ámbito de las Variables (Scope)**

El ámbito de una variable se refiere a la región de un programa donde esa variable es accesible. En Python, hay dos tipos principales de ámbitos:

- **Local**: Las variables definidas dentro de una función tienen un ámbito local, lo que significa que solo pueden ser accesadas y modificadas dentro de la función donde fueron creadas.
- **Global**: Las variables definidas fuera de todas las funciones tienen un ámbito global, lo que significa que pueden ser accesadas desde cualquier parte del programa. Sin embargo, para modificar una variable global dentro de una función, se debe declarar como global.

