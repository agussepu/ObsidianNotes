---
tags:
  - HackingTools
---
---
En caso que se muestre lo que ejecutamos en el output: Mediante burpsuite capturaremos la petición del servidor el cual usaremos mediante docker (https://github.com/jbarone/xxelab : 5000), al interceptar vemos que se tramita por POST una estructura en XML
![[Pasted image 20250114113712.png]]

Ahora usamos ctrl + r para enviarlo al repeter y lo enviamos para ver la respuesta
![[Pasted image 20250114114247.png]]

Vemos que en la respuesta nos devuelve ese campo, por lo que usando una entidad o DTD (Document Type Definition) podemos ejecutar el XML de manera que nos representa un archivo del servidor mediante una ruta absoluta
![[Pasted image 20250114133630.png]]
