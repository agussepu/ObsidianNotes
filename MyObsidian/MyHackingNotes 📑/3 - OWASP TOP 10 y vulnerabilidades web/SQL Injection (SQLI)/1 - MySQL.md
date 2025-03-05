---
tags:
  - HackingTools
---
---
Comandos comunes **SQL**
```mysql
-- muestra las bases de datos existentes
show databases;

-- seleccionar una base de datos
use mysql; -- nombre de la base de datos

-- mostrar tablas existentesd dentro de la base de datos
show tables;

-- Este comando se usa para mostrar la estructura de la tabla user en la base de datos que estés utilizando.
describe user;

-- Este comando se usa para consultar los valores reales de las columnas user y password de la tabla user.
select user,password from user;

-- Acotamos la busqueda para el usuario root de la tabla user
select user,password from user where user = 'root';

-- Crear un base de datos
create database Hack4u;

-- Creamos una tabla llamada users donde dentro del paretesis le indicaremos las columnas
create table users(id int(32),username varchar(32));

-- Eliminar tabla
drop table users;

-- Introducir datos a la tabla y sus respectivos valores
insert into users(id ,username,password) values(1,'admin','admin123$!');

-- cambiar un valor de una seccion de una columna
update users set id=3 where username='s4vitar';

-- mostrar todas las columnas de una tabla;
select * from users;

-- Creamos un usuario llamado s4vitar con contraseña s4vitar123
CREATE USER 's4vitar'@'localhost' IDENTIFIED BY 's4vitar123';

-- le damos privilegios al nuevo usuario en la base de datos hack4u
grant all privileges on Hack4u.* to 's4vitar'@'localhost';

-- ctrl d para salir
```

