---
tags:
  - Python
---
---
La Programación Orientada a Objetos (POO) es un paradigma de programación que utiliza objetos y clases en su enfoque central. Es una manera de estructurar y organizar el código que refleja cómo los desarrolladores piensan sobre el mundo real y las entidades dentro de él.

**Clases**

Las clases son los fundamentos de la POO. Actúan como plantillas para la creación de objetos y definen atributos y comportamientos que los objetos creados a partir de ellas tendrán. En Python, una clase se define con la palabra clave ‘**class**‘ y proporciona la estructura inicial para todo objeto que se derive de ella.

**Instancias de Clase y Objetos**

Un objeto es una instancia de una clase. Cada vez que se crea un objeto, se está creando una instancia que tiene su propio espacio de memoria y conjunto de valores para los atributos definidos por su clase. Los objetos encapsulan datos y funciones juntos en una entidad discreta.

**Métodos de Clase**

Los métodos de clase son funciones que se definen dentro de una clase y solo pueden ser llamados por las instancias de esa clase. Estos métodos son el mecanismo principal para interactuar con los objetos, permitiéndoles realizar operaciones o acciones, modificar su estado o incluso interactuar con otros objetos.

```python
#!/usr/bin/python3
class Persona: #Clase
	def __init__(self,nombre,edad): #metodo
		self.nombre = nombre
		self.edad = edad
	def saludo(self):               #metodo
		return f"hola soy {self.nombre}, y tengo {self.edad}"
		
marcelo = Persona("marcelo",28)
print(marcelo.saludo())
```

También podemos dar valores por defecto a los métodos en caso que no se le de un valor al iniciarlo
```python
class CuentaBanco():

	def __init__(self,cuenta,dinero=0):
		self.cuenta = cuenta
		self.dinero = dinero
		
miCuenta = CuentaBanco(1234)
print(miCuenta.dinero) # --> 0
```