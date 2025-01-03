---
tags:
  - Redes
aliases:
  - mac
---
La dirección MAC es un número hexadecimal de **12 dígitos** (número binario de **6 bytes**), que está representado principalmente por **notación hexadecimal** de dos puntos.

Los primeros **6 dígitos** (digamos **00:40:96**) del MAC Address identifican al fabricante, llamado ***OUI*** (**Identificador Único Organizacional**). El Comité de la Autoridad de Registro de **IEEE** asigna estos prefijos MAC a sus proveedores registrados.

Los seis dígitos más a la derecha (***NIC***) representan el **controlador de interfaz de red**, que es asignado por el fabricante.

Es decir, los primeros **3 bytes** (**24 bits**) representan el fabricante de la tarjeta, y los últimos **3 bytes** (**24 bits**) identifican la tarjeta particular de ese fabricante. Cada grupo de **3 bytes** se puede representar con **6 dígitos hexadecimales**, formando un número hexadecimal de **12 dígitos** que representa la MAC completa.

Para una búsqueda de fabricante utilizando direcciones MAC, se requieren al menos los primeros **3 bytes** (**6 caracteres**) de la dirección MAC. Una de las herramientas que vemos en esta clase para lograr dicho fin es ‘[**macchanger**](https://www.kali.org/tools/macchanger/)‘, una herramienta de GNU/Linux para la visualización y manipulación de direcciones MAC.

``` bash  
❯ arp-scan -I wlan0 --localnet
Interface: wlan0, type: EN10MB, MAC: 74:97:79:b6:78:b1, IPv4: 192.168.2.105
Starting arp-scan 1.10.0 with 256 hosts (https://github.com/royhills/arp-scan)
192.168.2.1	1c:a0:d3:62:16:88	Intertecno SRL "NISUTA"

1 packets received by filter, 0 packets dropped by kernel
Ending arp-scan 1.10.0: 256 hosts scanned in 2.046 seconds (125.12 hosts/sec). 1 responded
```