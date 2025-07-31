---
tags:
  - HackingTools
---
---
En caso de que a la hora de poner una comilla en la query esta devuelve un error esto puede indicar que es vulnerable a dicho ataque, aunque esta la posibilidad que no veamos el error en pantalla pero la vulnerabilidad si este presente. (recodar que la inyeccion no siempre comienza por una ' depende de como este montada la web)
![[orderbysql.png]]

En caso que no se vea el error podemos usar `sleep` para ver si es vulnerable en caso que demore lo que le indiquemos sabemos que es vulnerable
![[sleepsqli.png]]

Comentamos luego del 100 para cerrar la query ademas debemos ordenar mediante `order by` ya que debemos hacer fuzzing para encontrar la cantidad de columnas que existen (debemos como atacantes encontrar ese numero) ya que al cononcer ese numero podemos usar `union select`
![[unionselect2.png]]
En este usamos `union select 1` ya que hay una sola columna en caso que sean 3 usamos `union select 1,2,3` y así con la cantidad de columnas que hayan. Podemos usar querys dentro de la web como `union select databases()` y nos mostrara la base de datos que se esta utilizando actualmente

En caso de querer ver todas las bases de datos usamos la siguiente query `schema_name from information_schema-schemata` y usaremos `groups_concat()` para que nos muestre todas las bases de datos separadas por coma
![[unionselectgroup.png]]

La query para que te muestre todas las tablas de una base de datos es la siguiente `groups_concat(table_name) from information_schema.tables where table schema='Hack4u'` (en este caso la base de datos se llama Hack4u)
![[Pasted image 20250110231935.png]]

La query para que te muestre todas las columnas de una tabla de una base de datos es `groups_concat(column_name) from information_schema.columns where table schema='Hack4u' and table_name='users'`
![[Pasted image 20250110232309.png]]

En caso de haber muchas columnas, bases de datos o tablas podemos jugar con `limits 0,1` para que nos muestre solo algunas 

Para este punto ya conociendo las columnas de una tabla de una base de datos podemos listar el contenido de las mismas (en este caso las columnas user)
![[Pasted image 20250110233408.png]]

en esta ocasion nos encontrabamos en la base de datos Hack4u donde tambien se encuentra la tabla users pero en caso de querer ver el contenido de otra base de datos deberiamos de haber puesto `otraBasedeDatos.users`
![[Pasted image 20250110233621.png]]

![[Pasted image 20250110233657.png]]
