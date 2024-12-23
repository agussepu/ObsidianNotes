---
tags:
  - Git
---
---
En caso de escribir mal el comentario de un commit podemos usar `git commit --amend` para cambiar el comentario del ultimo commit

En caso de querer modificar el ultimo commit cambiandole el comentario y ademas agregando algun archivo que quedo pendiente tambien podemos usar `git commit --amend` solo que debemos agregar al area de staged el archivo que queremos agregar y una vez usado el comando anterior agregara el nuevo comentario y lo que este en el area de staged al commit anterior

(tengamos en cuenta que al hacer lo anterior no es exactamente el mismo commit es otro que remplaza este)

Si queremos modificar un commit mas antiguo que no sea el ultimo que hicimos es mas complicado y no es tan recomendable ya que al hacer esto movemos el head hacia atras y este borrara todo lo que hay adelante del head en cuestion

Para cambiar un commit anterior escribimos `git rebase -i head~2->(numerodelcommit_a_moficar)`
luego en vs code elegimos el commit a modificar y escribimos edit
![[Pasted image 20240812191506.png]]
![[Pasted image 20240812191520.png]]

Y ahora debemos usar el proceso de git amend anteriormente visto para cambiar lo que queramos y para finalizar debemos usar `git rebase continue`
![[Pasted image 20240812191934.png]]
![[Pasted image 20240812192048.png]]
