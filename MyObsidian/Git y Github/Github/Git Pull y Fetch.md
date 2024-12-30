---
tags:
  - Git
---
 ---
Usando `git pull` podemos bajar los cambios que se hayan hecho en el repositorio remoto a nuestra pc local
en caso de no funcionar bien podemos usar `git pull origin master`. Lo que hace el git pull en realidad es primero hacer un git fetch y luego un git merge hace ambos procesos por lo que primero baja los archivos del servidor y luego los fusiona directamente a la rama. Por lo que al usar git pull el proceso es mas rapido pero tenemos menos control

Por lo que podemos usar tambien `git fetch` bajando solamente los archivos del servidor sin fusionarlo con nuestras ramas locales teniendo mas control