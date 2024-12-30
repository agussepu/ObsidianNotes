---
tags:
  - Linux
---
Para buscar todo usamos 
```bash
ls -l *.png

# Para que nos complete la busqueda
ls -l fotoDe*

# Buscamos todos las extensiones con ese nombre de archivo
ls foto.*
```

Para buscar con un caracter especifico general
```bash
ls -l foto?.png
>foto1.png
>foto2.png

#Tambien podemos buscar varios juntos
ls -l foto??.jpg
```

Para buscar por letras especificas:
```bash
# Buscara todos los archivos que comiencen por estas letras en miniscula
ls -l [ci]*


# buscara el rango de 2 a 6
ls -l foto[2-6]*
>foto2.png
>foto3.png
# Buscara el rango de A a la Z
ls -l foto[A-Z]*
```