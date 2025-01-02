---
tags:
  - Linux
---
---
***Grep***: 
grep -v tambien podemos quitar en vez de buscar


---
***Find***: Estructura básica `find <startingdirectory> <options> <search term>`

- **Por nombre:** 
	- *-name*: Distingue de mayúscula y minúscula `find . -name my-file`
	- *-iname*: No distingue de minúscula y mayúscula
	- *-not*: Busca excluyendo una palabra
- **Por formato**: `find . -name “*.txt”`
- **Por tipo**: 
	- *d*  directorio o carpeta
	- *f*  archivo normal
	- *l*  enlace simbólico
	- *c*  dispositivos de caracteres
	- *b*  dispositivos de bloque
	Un ejemplo simple del uso del tipo de archivo para la búsqueda se puede ver a continuación: --> `find / -type d`

Mas info: (fechas, tamaño,etc)
https://www.hostinger.es/tutoriales/como-usar-comando-find-locate-en-linux/