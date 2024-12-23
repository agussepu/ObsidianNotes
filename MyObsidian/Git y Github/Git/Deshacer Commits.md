---
tags:
  - Git
---
---
Para hacer este tipo de operaciones usamos el `git reset` y hay tres maneras de usarlo:
- *La forma blanda* (`git reset --soft <hash_del_commit>`): mediante este comando movemos el head el commit mas atras que querramos, hay que tener en cuenta que al hacer esto borrara los commits mas nuevos que al que nos movimos y traera la informacion de estos al area de staged. Otra forma de indicar que commir queremos modificar es con la notacion relativa usando `git reset --soft head~2` el dos indica la cantidad de pasos atras a partir del head en este caso hira dos commits atras (deja todo y si tiene que sobreescribir archivos lo hace)

- *La forma mas agresiva*  `git reset --mixed <hash_del_commit>`: Este mueve el head, borra los commits superiores, deja el area de trabajo como la teniamos, pero borra todo lo que habia en el area de staged }

- *La forma hard* `git reset --hard <hash_del_commit>` : muvee el punto o head y sobreescribe todo y trae todo lo de los commits anteriores a el area de trabajo, ademas borra todo lo del area de staged