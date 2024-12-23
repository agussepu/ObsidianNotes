---
tags:
  - Git
---
---
Usando git restore podemos restaurar archivos que se encuentren dentro del area de preparacion
![[Pasted image 20240810175219.png]]

Con git checkout restauramos el archivo al ultimo commit o al ultimo backup que hicimos del mismo, en este caso modificaremos con nano un archivo y luego lo restauramos a exactamente como estaba antes ( solo restaura en caso de no haberlo subido al area de preparacion como vemos aca en ningun momento se hizo un git add)
![[Pasted image 20240810175715.png]]

En caso de haberlo subido al area de preparacion usaremos `git reset --hard` usar esto puede ser una mala practica ya que descarta los cambios del repositorio y los del area de staged (area de preparacion)

