---
tags:
  - Linux
---
 ---
Para crear usuarios y grupos y asignar usuarios a grupos en Linux desde la línea de comandos, puedes utilizar varios comandos específicos. Aquí tienes los pasos básicos:
### ***Crear un nuevo grupo***:
Puedes utilizar el comando `groupadd` para crear un nuevo grupo. Por ejemplo:

```bash
sudo groupadd nombre_grupo
```
### ***Crear un nuevo usuario:***
Puedes usar el comando `useradd` para crear un nuevo usuario. Por ejemplo:

```bash
sudo useradd -s /bin/bash nombre_usuario -d /home/pepe
```

 - -s: asigna la shell del usuario
 - -d: asigna el directorio del usuario
### ***Asignar contraseña al nuevo usuario:***
Para asignar una contraseña al nuevo usuario, utiliza el comando `passwd`. Por ejemplo:

```bash
sudo passwd nombre_usuario
```
### ***Asignar usuario a un grupo:***
Puedes utilizar el comando `usermod` para añadir un usuario existente a un grupo específico. Por ejemplo:

```bash
sudo usermod -aG nombre_grupo nombre_usuario
```

