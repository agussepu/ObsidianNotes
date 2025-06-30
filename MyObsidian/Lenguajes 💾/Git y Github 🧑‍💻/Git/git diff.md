---
tags:
  - Git
---
---
Con `git show` podemos ver la informacion de un archivo el cual ya se mando mediante un commit 

Con `git diff` podemos comparar lo que hay en el area de preparacion con el ultimo commit (rojo=commit, verde=staged)
![[Pasted image 20240810192952.png]]

Para poder comparar dos commits debemos primero buscar la identificacion del commit con `git log` o tambien podemos usar `git log --oneline`
![[Pasted image 20240810193430.png]]
![[Pasted image 20240810193745.png]]
Con los primeros numeros del hash podemos identificar el commit pero el problema es que en caso de estar trabajando con grandes cantidades de commits exite la posibilidad que se repitan por lo que podemos modificar la extension minima del hash con `git config --global core.abbrev <numcaracteres>` 

Como vemos aca se pueden ver la diferencia entre el segundo y tercer commit
![[Pasted image 20240810194713.png]]

Tambien podemos usar `git diff --name-only hash1 hash2` para q solo nos muestre el nombre de los archivos que cambiaron entre los commits ![[Pasted image 20240810195312.png]]

Y tambien podemos ver los cambios linea por linea con `--word-diff` bastante util para trabajar con codigo
![[Pasted image 20240810195707.png]]