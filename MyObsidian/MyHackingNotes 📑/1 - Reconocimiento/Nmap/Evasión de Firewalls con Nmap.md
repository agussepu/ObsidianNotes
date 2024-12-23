---
tags:
  - Reconocimiento
  - HackingTools
aliases:
  - Evasion de firewalls
  - tecnicas nmap
---
----
Cuando se realizan pruebas de penetración, uno de los mayores desafíos es evadir la detección de los **Firewalls**, que son diseñados para proteger las redes y sistemas de posibles amenazas. Para superar este obstáculo, Nmap ofrece una variedad de técnicas de evasión que permiten a los profesionales de seguridad realizar escaneos sigilosos y evitar así la detección de los mismos.

Algunos de los parámetros vistos en esta clase son los siguientes:

- **MTU (–mtu)**: La técnica de evasión de **MTU** o “**Maximum Transmission Unit**” implica ajustar el tamaño de los paquetes que se envían para evitar la detección por parte del Firewall. Nmap permite configurar manualmente el tamaño máximo de los paquetes para garantizar que sean lo suficientemente pequeños para pasar por el Firewall sin ser detectados.

- **Data Length (–data-length)**: Esta técnica se basa en ajustar la **longitud de los datos** enviados para que sean lo suficientemente cortos como para pasar por el Firewall sin ser detectados (ya que muchas veces los firewalls saben de que tamaño son los paquetes utilizados para hacerles reconocimiento ). Nmap permite a los usuarios configurar manualmente la longitud de los datos enviados para que sean lo suficientemente pequeños para evadir la detección del Firewall.
```bash 
 sudo nmap -p80 192.168.2.1 --data-length 21 #se le suma 21 al tamaño que tenga el paquete enviado por nmap
```

- **Source Port (–source-port)**: Esta técnica consiste en configurar manualmente el número de **puerto de origen** de los paquetes enviados para evitar la detección por parte del Firewall. Nmap permite a los usuarios especificar manualmente un puerto de origen aleatorio o un puerto específico para evadir la detección del Firewall.
	esto se hace ya que muchas veces hay una lista blanca de los puertos los cuales se pueden comunicar con dicho objetivo y a la hora de enviar un paquete nuestro sistema abre un puerto aleatorio y con este parametro podes especificar que puerto abre temporalmente para hacer la petición y que no sea aleatorio
```bash 
sudo nmap -p80 192.168.2.1 --source-port 55
```

- **Decoy (-D)**: Esta técnica de evasión en Nmap permite al usuario enviar **paquetes falsos** a la red para confundir a los sistemas de detección de intrusos y evitar la detección del Firewall. El comando **-D** permite al usuario enviar paquetes falsos junto con los paquetes reales de escaneo para ocultar su actividad.
	Podremos emitir un paquete pero falsificar las ip dando come que múltiples ip ficticias están enviando paquetes aunque en realidad es una sola 
```bash 
sudo nmap -p- 192.168.2.113 -n -Pn -D 192.168.2.230 192.168.2.43 
```
 para ver los paquetes enviados a una ip destino en wireshark usar: ip.dst == 192.168.2.113

- **Fragmented (-f)**: Esta técnica se basa en **fragmentar los paquetes** enviados para que el Firewall no pueda reconocer el tráfico como un escaneo. La opción **-f** en Nmap permite fragmentar los paquetes y enviarlos por separado para evitar la detección del Firewall.
	en wireshark para ver los paquetes fragmentados usamos --> ip.flags.mf == 1

- **Spoof-Mac (–spoof-mac)**: Esta técnica de evasión se basa en **cambiar la dirección MAC** del paquete para evitar la detección del Firewall. Nmap permite al usuario configurar manualmente la dirección MAC para evitar ser detectado por el Firewall.
```bash 
sudo nmap -p80 192.168.2.1 --spoof-mac 11:22:33:44:55:66 -Pn
```

- **Stealth Scan (-sS)**: Esta técnica es una de las más utilizadas para realizar escaneos sigilosos y evitar la detección del Firewall. El comando **-sS** permite a los usuarios realizar un escaneo de tipo **SYN** **sin establecer una conexión completa**, lo que permite evitar la detección del Firewall.

- **min-rate (–min-rate)**: Esta técnica permite al usuario **controlar la velocidad de los paquetes** enviados para evitar la detección del Firewall. El comando **–min-rate** permite al usuario reducir la velocidad de los paquetes enviados para evitar ser detectado por el Firewall. (5000 es el min rate recomendado)
```bash
sudo nmap -p- --open -sS --min-rate 5000 192.168.2.1
```


Es importante destacar que, además de las técnicas de evasión mencionadas anteriormente, existen muchas otras opciones en Nmap que pueden ser utilizadas para realizar pruebas de penetración efectivas y evadir la detección del Firewall. Sin embargo, las técnicas que hemos mencionado son algunas de las más populares y amplia mente utilizadas por los profesionales de seguridad para superar los obstáculos que presentan los Firewalls en la realización de pruebas de penetración.