## awk
awk nos facilita el cortart por argumentos de manera sencilla con -> `awk '{print $1}'` despues del dolar pones el numero del argumento que queres

Mediante awk tambien podemos decirle que nos deje solo con una linea que nosotros querramos, por ejemplo de un output si solo queremos la segunda linea del mismo lo podemos asi de la siguente manera --> `awk '{NR==2}'` 

En caso de tener una argumento muy largo junto podemos poner delimitadores para separar por argumentos por ejemplo `192.168.0.1/24` para separarlo con el delimitador de / podemos con awk hacer lo siguiente `awk '{print $1}' FS="/"`

En caso de querer el ultimo argumento de todos podemos jugar con `awk 'NF{print $NF}'`

## tail y head
tail nos permitira quedarnos con la ultima linea de la siguiente manera `tail -n 1`
head nos permitira quedarnos con las primeras lineas por ejemplo con la primera `head -n 1`


tr podemos usarlo para remplazar, cambiar

wc -l

cut