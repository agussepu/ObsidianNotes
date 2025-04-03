```python
#!/usr/bin/python3

class Rectangulo():

	def __init__(self,alto, ancho):
		self.alto = alto
		self.ancho = ancho
	
	@property #accederemos a este metodo como una propiedad
	def area(self):
		return self.ancho * self.alto
	
	def __str__(self): # con este metodo especial definiremos que se muestre a la hora de mostrar el objeto
		return "Esto es un rectangulo"

rect1 = Rectangulo(5,4)
print(f"El area de rect1 es {rect1.area}")
print(rect1)

```

```python
#!/usr/bin/python3

class Libro:
		IVA = 0.21
	def __init__(self, titulo, autor, precio):
		self.titulo = titulo
		
		self.autor = autor
		
		self.precio = precio
		
	@staticmethod #no utiliza el self por lo tanto depende de la clase que declaremos sino de la general
	def bestseller(total_ventas):
		return total_ventas > 5000
		
	@classmethod # Dependera de cual clase general estemos usando
	def precio_con_iva(cls, precio):
		return precio + precio * cls.IVA

  
class LibroDigital(Libro):
	IVA = 0.10
	mi_libro = Libro("LibroUno","Agus",17.5)	
	mi_libro_digital = LibroDigital("LibroUno","Agus",17.5)

	print(f"\n[+] El precio del libro con IVA incluido es de {Libro.precio_con_iva(mi_libro.precio)}")

	print(f"\n[+] El precio del libro digital con IVA incluido es de {LibroDigital.precio_con_iva(mi_libro_digital.precio)}")
```

![[Pasted image 20250114195546.png]]