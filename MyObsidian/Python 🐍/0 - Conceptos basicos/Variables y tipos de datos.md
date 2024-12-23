---
aliases:
  - tipos de datos
---
---
Las variables en Python son como nombres que se le asignan a los datos que manejamos. Piensa en una variable como un nombre que pones a un valor, para poder referirte a él y utilizarlo en diferentes partes de tu código.

En la clase actual, vamos a enfocarnos en comprender las variables y algunos de los tipos de datos fundamentales en Python. Estos conceptos son esenciales, ya que nos permiten almacenar y manipular la información en nuestros programas.

**Variables**

Una variable en Python es como un nombre que se le asigna a un dato. No es necesario declarar el tipo de dato, ya que Python es inteligente para inferirlo.

**Cadenas (Strings)**

Las cadenas son secuencias de caracteres que se utilizan para manejar texto. Son inmutables, lo que significa que una vez creadas, no puedes cambiar sus **caracteres individuales**.

**Números**

Python maneja varios tipos numéricos, pero nos centraremos principalmente en:

- **Enteros (Integers)**: Números sin parte decimal.
- **Flotantes (Floats)**: Números que incluyen decimales.

```python
  1 #!/usr/bin/python3
  2 
  3 #Cadenas
  4 cadena = "mi cadena"
  5 ip_address = "192.168.2.1"
  6 
  7 print(cadena)
  8 print(type(ip_address))
  9 
 10 #Enteros
 11 number = 4
 12 
 13 #Forzamos el 5 como flotante
 14 other_number = float(5)
 15 print(type(other_number))
 16 
 17 #Forzamos un numero a cadena
 18 chain = str(4)
 19 print(type(chain))
 20 
 21 #Forzamos un entero
 22 final_number = int(5.0)
 23 print(type(final_number))
```

**Listas**

Las listas son colecciones ordenadas y mutables que pueden contener elementos de diferentes tipos. Son ideales para almacenar y acceder a secuencias de datos.

Y para trabajar con estas listas, así como con cadenas y rangos de números, utilizaremos los bucles ‘**for**‘, que nos permiten iterar sobre cada elemento de una secuencia de manera eficiente.

Estas son solo algunas de las estructuras de datos con las que trabajaremos por el momento. A medida que avancemos en las próximas clases, exploraremos más tipos de datos y estructuras más complejas, ampliando nuestras herramientas para resolver problemas y construir programas más sofisticados.

```python
#listas

my_ports = [22, 80, 443, 8080]

for port in my_ports:
	print(f"Este es el puerto: {port}")
print(f"\n[+] La lista tiene un total de {len(my_ports)} elementos")
```

```python
#metodos

my_ports = [12, 22, 80, 443, 8080, 12]
my_ports += [87, 79]

#agrefa al final de la lista el elemento dado
my_ports.append(22)

#sorted ordena la lista
my_ports = sorted(my_ports)

#insertamos el numero 5 en el indice 2
my_ports.insert(2, 5)

#borramos el ultimo elemento de la lista
my_ports.pop()

#Buscamos el indice del elemento 443 en nuestra lista
my_ports.index(443)

#contar cantidad de veces q se repetite un elemento
my_ports.count(12)

#maximo, minimo y tamaño
print(f"\n[+] El numero mas alto de la lista es {max(my_ports)}")
print(f"\n[+] El numero mas bajo de la lista {min(my_ports)}")
print(f"\n[+] El tamaño de la lista {len(my_ports)}")

#Calculo de la media con suma y tamaño
promedio = (sum(my_ports) / len(my_ports) )
print(f"\n[+] EL promedio de la lista es {round((promedio),1)}")

#muestra del indice 0 al 3
print(my_ports[0:3])
print(my_ports[:3])

#del 2 en adelante
print(my_ports[2:])

#del final
print(my_ports[-1])

```

```python
my_ports = [12,22, 80, 443, 12, 8080, 12]
my_ports += [87, 79]
  
for port in my_ports:
	print(f"Este es el puerto: {port}")
	print(f"\n[+] La lista tiene un total de {len(my_ports)} elementos")

#iterar entre el indice y el valor del elemento
for x,y in enumerate(my_ports):
	print(f"{x} : {y}")

#Busco el indice de los elementos repetidos nuemros 12
indices = [x for x,y in enumerate(my_ports) if y == 12]
print(indices)
```

