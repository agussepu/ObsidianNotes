---
tags:
  - Git
---
---
Inicializamos git en un directorio con `git init`

esto crea una carpeta oculta .git que almacena todo lo necesario para su uso
![[got.png]]

Usamos git add para añadir los archivos al area de preparacion
```bash
git add prueba.txt
git add . #para añadir todo
```

Mediante git status podemos ver el estado de las cosas añadidas al area de preparacion y en caso de querer sacar un archivo de este area usamos `rm --cached <filename>` para en caso de hacer el commit no subirlo
Tambien podemos usar un git status que nos muestre solo lo necesario en este caso usaremos `git status -s` (-s = short)
![[Pasted image 20240810173035.png]]

En este caso vemos que hay un nuevo archivo que no subimos al area de preparacion (untracked files, quiere decir que git no le esta haciendo seguimiento a este archivo)
![[Pasted image 20240810173306.png]]

Ahora usaremos `git commit` para subir todo lo del area de preparacion al repositorio (usamos el -m para agregarle un mensaje al commit y -a para poner todo en el area de prepaparacion directamente)
![[Pasted image 20240810173818.png]]
En caso de no poner el -m nos mandara a vscode para escribir el comentario para el commit ( a veces es mejor hacer esto en caso de querer poner largas descripiciones de los commits)