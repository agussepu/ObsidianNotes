---
tags:
  - Python
---
---
La configuración básica para poder hacer aparecer una ventana en pygame es la siguiente
```python
import pygame
from sys import exit #lo usamos para cerrar el programa

#Iniciamos el modulo pygame
pygame.init()

#Tamaño de la ventana
screen = pygame.display.set_mode((800,600))

#Titulo de la ventana
pygame.display.set_caption("TaTeTi")

#Inicizamos un reloj para controlar los fps
clock = pygame.time.Clock() 

while True:
	#eventos
	for event in pygame.event.get():
		# evento de salida		
		if event.type == pygame.QUIT:
		pygame.quit()
		exit()

	#refresh
	
	pygame.display.update() #actualiza la pantalla
	#techo de fps
	clock.tick(60)
```

Algunos eventos comunes a la hora de usa pygame son los siguentes
![[Pasted image 20250316155717.png]]

bibliografia:https://www.youtube.com/watch?v=AY9MnQ4x3zk&t=2155s