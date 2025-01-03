---
tags:
  - Redes
aliases:
  - Calculo subneting
---
---
Técnicas adicionales para calcular velozmente el Network ID, la máscara de red y la Broadcast Address, en base a una dirección **[[IPV4 - IPV6|IP]]** y **[[Subnetting|CIDR]]** que el cliente nos pase. De esta forma, no será necesario hacer uso del Excel que previamente construimos, logrando tener en un menor tiempo los valores correspondientes a cada componente de direccionamiento.

1) 172.14.15.16/17
2) Pasamos la ip a binario --> 10101100.00001110.00001111.00010000 ( 172.14.15.16 )
 ``` bash  
❯ echo "$(echo "obase=2;172" | bc)"
10101100
❯ echo "$(echo "obase=2;14" | bc)"
1110
❯ echo "$(echo "obase=2;15" | bc)"
1111
❯ echo "$(echo "obase=2;16" | bc)"
10000
```
3) Mascara de Red: /17 por lo que la red seran los primero 17 bits
	11111111.11111111.10000000.00000000 --> 255.255.128.0
	Para averiguar aquellos octetos que no sean todos ceros o todos uno usamos:
	```bash
	❯ echo "$(echo "ibase=2;10000000" | bc)"
	128
	```
4)  Network ID: sumamos los binarios de la mascara y la ip
	10101100.00001110.00001111.00010000
	11111111.11111111.10000000.00000000
	 --------------------------------------
	 10101100.00001110.00000000.0000000 --> network id en binario
	 ```bash
	❯ echo "$(echo "ibase=2;10101100" | bc)"
	172
	# y asi con cada octeto nos daria la network id
	```
	Network id --> 172.14.0.0

5) Broadcast Adress  --> restamos 32 (que es el total de bits de la ip) menos 17 (que seria el CIDR /17) que nos da 15 bits que vamos agregar desde final de el network id
	10101100.00001110.00000000.0000000 y agrgandole los 15 bits nos quedaria
	10101100.00001110.01111111.11111111 --> esto es el broadcast address en binario y si lo pasamos a decimal nos da 172.14.127.255

En resumen la operatoria seria asi:
![[Subneteo_image.png]]