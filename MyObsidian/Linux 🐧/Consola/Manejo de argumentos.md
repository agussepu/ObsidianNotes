## awk
awk nos facilita el cortar por argumentos de manera sencilla con -> `awk '{print $1}'` después del dólar pones el numero del argumento que quieres

Mediante awk también podemos decirle que nos deje solo con una linea que nosotros queramos, por ejemplo de un output si solo queremos la segunda linea del mismo lo podemos asi de la siguiente manera --> `awk '{NR==2}'` 

En caso de tener una argumento muy largo junto podemos poner delimitadores para separar por argumentos por ejemplo `192.168.0.1/24` para separarlo con el delimitador de / podemos con awk hacer lo siguiente `awk '{print $1}' FS="/"`

En caso de querer el ultimo argumento de todos podemos jugar con `awk 'NF{print $NF}'`

## tail y head
tail nos permitirá quedarnos con la ultima linea de la siguiente manera `tail -n 1`
head nos permitirá quedarnos con las primeras líneas por ejemplo con la primera `head -n 1`


## tr
tr podemos usarlo para remplazar -> ``tr ' ' ','`` remplazamos espacios por comas

## rev
rev invierte toda la cadena 

wc -l

cut

## sort
Ordena alfabeticamante el output

## uniq
con uniq -u nos devuelve la cadena que no se repite

## Strings
Nos lista unicamente las cadenas de caracteres de un archivo imprimibles

## file 
nos devuelve el tipo de archivo al cual apuntamos