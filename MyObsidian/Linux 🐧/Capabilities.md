---
aliases:
  - Capabilities
---
---
Las capabilities nos permiten gestionar que permisos tiene un proceso para acceder a las partes del kernel. Independientemente del usuario que lo lance.  
Existen una serie de capabilities que se pueden habilitar a los programa para que tengan acceso a dichas partes que gestionan.  
Estos cuentan con Flags para poder determinar que acciones están disponibles:  

Efectivas (e): las capacidades usadas por el núcleo para llevar a cabo comprobaciones de permisos para el proceso.

Permitidas (p): la capacidades que el proceso puede asumir (esto es, un superconjunto limitante para los conjuntos de efectivas y heredadas). Si un proceso elimina una capacidad de su conjunto de permitidas, no puede volver nunca a adquirir esa capacidad (a menos que ejecute un programa set-UID-root).

Heredadas (i): las capacidades que se conservan tras llamadas a execve(2)

Para listar la capabiliestes del sistema ejecutamos `getcap -r / 2>/dev/null`

Para asignar una capabilieti usamos `setcap cap_setuid+ep /usr/bin/python3.11` -> esta capabilitie nos permite cambiar el UID (User ID) lo que nos permitiria escalar a root siendo un usuario x

Y para sacar la capabilietie lo hacemos con `setcap -r /usr/bin/python3.11`

En esta pagina [# GTFOBins](https://gtfobins.github.io/#+capabilities) podemos ver aquellos binarios que en caso de tener una capabilitie se puede llegar a tensar...
![[capabilities-image.png]]