---
aliases:
  - SUID
  - SGID
---
---
Los permisos SUID y SGID nos permiten ejecutar temporalmente un binario como el propietario en caso de SUID y como el grupo en caso de ser SGID esto puede ser una vulnerabilidad debiado a una posible escala de privilegios por parte de un atacante sabiendo que pueden ejecutar comandos de manera temporal 

Para buscar binarios SUID en el sistema lo hacemos asi -> `find / -type f -perm -4000 2>/dev/null`

Para buscar binarios SGID en el sistema lo hacemos asi -> `find / -type f -perm -2000 2>/dev/null`
## Permiso SGID
El permiso SGID está relacionado con los grupos, tiene dos funciones:

- Si se establece en un **archivo**, permite que cualquier usuario ejecute el archivo como si fuese miembro del grupo al que pertenece el archivo.
- Si se establece en un **directorio**, a cualquier archivo creado en el directorio se le asignará como grupo perteneciente, el grupo del directorio.

Para los directorios, la lógica del SGID y el motivo de su existencia es por si trabajamos en grupo, para que todos podamos acceder a los archivos de las demás personas. Si SGID no existiera, cada persona cada vez que crease un archivo, tendría que cambiarlo del grupo suyo al grupo común del proyecto. Asimismo, evitamos tener que asignarle permisos a «Otros».

**¿Cómo identificamos el permiso SGID?**
Cuando se asigna el permiso SGID, podemos notarlo porque en los permisos, en la parte de grupo, en el permiso de ejecución se asignará una `s`. Ojo, aquí hay que hacer dos distinciones:

![[SGID-image.png]]
Esto realmente para los directorios no tiene relevancia, solo para los archivos. En cualquier caso, esta característica de `s` mayúscula o minúscula dependiendo del permiso de ejecución se aplica siempre, incluido en el permiso SUID.

**¿Cómo activamos SGID?**
Para activarlo podemos usar cualquiera de los siguientes dos comandos:

- `chmod g+s <archivo>`
- `chmod 2*** <archivo>`

Siendo el `*` los permisos normales. (Ejemplo: `chmod 2755`)

## Permiso SUID

El permiso SUID permite que un archivo se ejecute como si del propietario se tratase, independientemente del usuario que lo ejecute, el archivo se ejecutará como el propietario. Ejemplo:

![[SUID-image.png]]

Al asignar permisos SUID, la salida del comando whoami, a pasado de ser sikumy a ser root. Esto porque como podemos ver, el propietario del binario de whoami, es root. Por lo tanto, está ocurriendo exactamente la definición que hemos dado arriba.

Eso si, una cosa a tener en cuenta y bastante importante, es que el permiso SUID no funciona en scripts, solo lo hace en binarios compilados. Esto se hace por razones de seguridad. En cualquier caso si quisieseis habilitar la ejecución de un script como otro usuario, siempre se puede tirar de sudo.

Ya lo vemos arriba, pero la forma de identificar el permiso SUID es mediante una `s` en el permiso de ejecución de los permisos del propietario. Aquí se aplica lo mismo que hemos mencionado en SGID, si el propietario no tiene permisos de ejecución, pero si permiso SUID, se verá como una `S` mayúscula, de lo contrario, minúscula, que es como debería de estar.

**¿Y qué ocurre con el permiso SUID en los directorios?**

El SUID no aplica a los directorios debido a que no hay una razón convincente de por qué debería. No puede funcionar de la misma manera que SGID. Linux no permite que un usuario entregue un archivo a otro usuario, el único capaz de hacer esto es root. Es decir, si yo soy el usuario sikumy, aunque yo sea el propietario de un archivo, no seré capaz de usar chown para entregar el archivo al usuario JuanSec, esta acción solo la puede hacer root.

**¿Cómo activamos SUID?**

Podemos hacerlo con alguno de los dos siguientes comandos:

- `chmod u+s <archivo>`
- `chmod 4*** <archivo>`

Siendo el `*` los permisos normales (Ejemplo: `chmod 4755`).

> Para indagar mas sobre [SUID y SGID](https://deephacking.tech/permisos-sgid-suid-y-sticky-bit-linux/#sgid)