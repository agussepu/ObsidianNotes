---
aliases:
  - Docker
tags:
  - Docker
---
---
**Docker** es una plataforma de **contenedores** de software que permite crear, distribuir y ejecutar aplicaciones en entornos aislados. Esto significa que se pueden empaquetar las aplicaciones con todas sus dependencias y configuraciones en un contenedor que se puede mover fácilmente de una máquina a otra, independientemente de la configuración del sistema operativo o del hardware.

Algunas de las ventajas que se presentan a la hora de practicar hacking usando Docker son:

- **Aislamiento**: los contenedores de Docker están aislados entre sí, lo que significa que si una aplicación dentro de un contenedor es comprometida, el resto del sistema no se verá afectado.
- **Portabilidad**: los contenedores de Docker se pueden mover fácilmente de un sistema a otro, lo que los hace ideales para desplegar entornos vulnerables para prácticas de hacking.
- **Reproducibilidad**: los contenedores de Docker se pueden configurar de forma precisa y reproducible, lo que es importante en el hacking para poder recrear escenarios de ataque.

docker ps --> contendores
docker images  --> imagenes

Para instalar **Docker** en Linux, se puede utilizar el comando “**apt install docker.io**“, que instalará el paquete Docker desde el repositorio de paquetes del sistema operativo. Es importante mencionar que, dependiendo de la distribución de Linux que se esté utilizando, el comando puede variar. Por ejemplo, en algunas distribuciones como CentOS o RHEL se utiliza “**yum install docker**” en lugar de “**apt install docker.io**“.

Una vez que Docker ha sido instalado, es necesario iniciar el **demonio** de Docker para que los contenedores puedan ser creados y administrados. Para iniciar el demonio de Docker, se puede utilizar el comando “**service docker start**“. Este comando iniciará el servicio del demonio de Docker, que es responsable de gestionar los contenedores y asegurarse de que funcionen correctamente.

Durante la clase, se mostrará cómo verificar que Docker ha sido instalado correctamente, además de comprobar si el demonio de Docker está en ejecución.

Un archivo **Dockerfile** se compone de varias secciones, cada una de las cuales comienza con una **palabra clave** en **mayúsculas**, seguida de uno o más argumentos.

Algunas de las secciones más comunes en un archivo Dockerfile son:

- **FROM**: se utiliza para especificar la imagen base desde la cual se construirá la nueva imagen.
- **RUN**: se utiliza para ejecutar comandos en el interior del contenedor, como la instalación de paquetes o la configuración del entorno.
- **COPY**: se utiliza para copiar archivos desde el sistema host al interior del contenedor.
- **CMD**: se utiliza para especificar el comando que se ejecutará cuando se arranque el contenedor.

Además de estas secciones, también se pueden incluir otras instrucciones para configurar el entorno, instalar paquetes adicionales, exponer puertos de red y más.

En esta clase, se mostrará cómo crear un archivo Dockerfile desde cero, además de ver cómo utilizar las diferentes secciones y palabras clave para configurar la imagen. En la siguiente clase, veremos cómo construir y ejecutar un contenedor a partir de la imagen creada
