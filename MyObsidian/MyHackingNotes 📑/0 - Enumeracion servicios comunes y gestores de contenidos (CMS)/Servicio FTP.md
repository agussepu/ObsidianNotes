---
tags:
  - HackingTools
---
---
**FTP** es un protocolo ampliamente utilizado para la **transferencia de archivos** en redes. La enumeración del servicio FTP implica recopilar información relevante, como la versión del servidor FTP, la configuración de permisos de archivos, los usuarios y las contraseñas (mediante ataques de fuerza bruta o guessing), entre otros.

Con ftp tenemos dos posibilidades que podamos entrar como invitados con el usuario anonymous el cual no necesita contraseña o con un usuario y contraseña preexistente que deberemos descubrir

# FTP con usuario y contraseña
A continuación, se os proporciona el enlace al primer proyecto que tocamos en esta clase:

- **Docker-FTP-Server**: [https://github.com/garethflowers/docker-ftp-server](https://github.com/garethflowers/docker-ftp-server)


En esta clase usaremos el diccionario  rockyou.txt el cual esta en mi ruta  `cat /usr/share/SecLists/Passwords/Leaked-Databases/rockyou.txt` dicho diccionario tiene mas de 14 millones de contraseñas


en esta ocasión jugaremos con awk para ver una contraseña en este caso la de la linea 132 para ponerle esa contraseña a una maquina vulnerable y poder practicar fuerza bruta con Hydra 
```bash
❯ cat /usr/share/SecLists/Passwords/Leaked-Databases/rockyou.txt | awk "NR==132"
louise
```

por lo que le pondremos esa contraseña al docker con ftp
```d
docker run \
	--detach \
	--env FTP_PASS=louise \
	--env FTP_USER=agussepu \
	--name my-ftp-server \
	--publish 20-21:20-21/tcp \
	--publish 40000-40009:40000-40009/tcp \
	--volume /data:/home/user \
	garethflowers/ftp-server
```

como podemos ver con nmap el docker tiene abierto el puerto 21 --> ftp y ademas sabemos su versión
```bash
❯ nmap --top-ports 500 localhost -v -n -Pn
PORT    STATE SERVICE
20/tcp  open  ftp-data
21/tcp  open  ftp
22/tcp  open  ssh
631/tcp open  ipp

❯ nmap -p21 -sCV localhost -v -n -Pn
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 2.0.8 or later
```

por lo que con el comando `ftp localhost (o la ip que corresponda)` podemos conectarnos con dicho protocolo donde debemos brindar el usuario y la contraseña

Una de las herramientas que usamos en esta clase para el primer proyecto que nos descargamos es ‘**Hydra**‘. Hydra es una herramienta de pruebas de penetración de código abierto que se utiliza para realizar ataques de fuerza bruta contra sistemas y servicios protegidos por contraseña. La herramienta es altamente personalizable y admite una amplia gama de protocolos de red, como HTTP, FTP, SSH, Telnet, SMTP, entre otros.

Usaremos esta herramienta para descrubrir la constraseña del usuario del contendor que tiene abierto el puerto ftp 

usaremos los parámetros -L y -P (el parametro va en mayuscula si vas a indiciar un diccionario ya que no sabes el usuario o contraseña y en minuscula si es que sabes el usuario o contraseña)
```bash
❯ hydra -l agussepu -P /usr/share/SecLists/Passwords/Leaked-Databases/rockyou-15.txt ftp://127.0.0.1 -t 15
#el -t es para las tareas en paralelo

Hydra v9.5 (c) 2023 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2024-01-15 17:26:44
[DATA] max 15 tasks per 1 server, overall 15 tasks, 249 login tries (l:1/p:249), ~17 tries per task
[DATA] attacking ftp://127.0.0.1:21/
[21][ftp] host: 127.0.0.1   login: agussepu   password: louise
1 of 1 target successfully completed, 1 valid password found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2024-01-15 17:27:15
```

Por lo que ya tenemos el usuario y la contraseña y tenemos acceso al contenedor 

---

# FTP con usuario anonymous o invitado

El siguiente de los proyectos que utilizamos para desplegar el contenedor que permite la autenticación de usuarios invitados para FTP, es el proyecto ‘**docker-anon-ftp**‘ de ‘**metabrainz**‘. A continuación, se os proporciona el enlace al proyecto:

- **Docker-ANON-FTP**: [https://github.com/metabrainz/docker-anon-ftp](https://github.com/metabrainz/docker-anon-ftp)

Mediante nmap nos damos cuenta que el puerto 21 tiene el usuario anonymous activado
```bash
❯ nmap -p21 -sCV 127.0.0.1

PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 2.0.8 or later
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_Can't get directory listing: PASV IP 172.17.0.2 is not the same as 127.0.0.1
Service Info: Host: Welcome
```

Lo confirmamos con el scrip de nmap ftp-anon
``` bash
❯ nmap --script ftp-anon -p21 127.0.0.1
Starting Nmap 7.94 ( https://nmap.org ) at 2024-01-15 17:40 -03
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00011s latency).

PORT   STATE SERVICE
21/tcp open  ftp
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_Can't get directory listing: PASV IP 172.17.0.2 is not the same as 127.0.0.1
```