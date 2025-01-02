El algoritmo de codificación **Base64** no es un algoritmo de cifrado, se decodifica fácilmente y, por lo tanto, no debe utilizarse como un método de cifrado seguro. No recomiendo que utilicéis esta técnica para proteger datos confidenciales, ya que se puede tensar en cuestión de segundos. En tal caso, es recomendable emplear métodos de cifrado seguros.

- ***Cifrar en base64***: `cat encrip.txt | base64` también podemos hacer que lo muestre todo en una sola linea con -w 0
- ***Descifrar***: `cat encrip.txt | base64 -d `