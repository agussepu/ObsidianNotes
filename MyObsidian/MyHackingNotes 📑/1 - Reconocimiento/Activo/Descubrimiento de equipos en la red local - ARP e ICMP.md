---
aliases:
  - ARP
  - ICMP
tags:
  - Reconocimiento
  - HackingTools
---
---
El descubrimiento de equipos en la red local es una tarea fundamental en la gestión de redes y en las pruebas de seguridad. Existen diferentes herramientas y técnicas para realizar esta tarea, que van desde el escaneo de puertos hasta el análisis de tráfico de red.

Entre los modos de escaneo que se explican en la clase, se encuentra el uso del parámetro ‘**-sn**‘ de Nmap, que permite realizar un escaneo de hosts sin realizar el escaneo de puertos. También se presentan las herramientas netdiscover, arp-scan y masscan, que utilizan el protocolo ARP para descubrir hosts en la red.

Cada herramienta tiene sus propias ventajas y limitaciones. Por ejemplo, **netdiscover** es una herramienta simple y fácil de usar, pero puede ser menos precisa que **arp-scan** o **masscan**. Por otro lado, **arp-scan** y **masscan** son herramientas más potentes, capaces de descubrir hosts más rápido y en redes más grandes, pero también son más complejas y pueden requerir más recursos.

En definitiva, el descubrimiento de equipos en la red local es una tarea fundamental para cualquier administrador de redes o profesional de seguridad de la información. Con las técnicas y herramientas adecuadas, es posible realizar esta tarea de manera efectiva y eficiente.

En este dispositivo mis mascara de subred es 255.255.255.0 por lo que con nmap puedo ver que dispositivos hay conectados a la red mediante un CIDR de /24
```bash
# Esta herramienta comprueba mediante pings ICMP
❯ nmap -sn 192.168.2.0/24
Starting Nmap 7.94 ( https://nmap.org ) at 2024-01-09 19:41 -03
Nmap scan report for _gateway (192.168.2.1)
Host is up (0.0089s latency).
MAC Address: 1C:A0:D3:62:16:88 (Intertecno SRL Nisuta)
Nmap scan report for agus-82yu (192.168.2.101)
Host is up.
Nmap done: 256 IP addresses (2 hosts up) scanned in 9.40 seconds
❯ nmap -sn 192.168.2.0/24 | grep -oP '\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}'
192.168.2.1
192.168.2.101
```

Otra alternativa que no funcione mediante pings es arp-scan el cual funciona mediante el envio de **solicitudes arp** 
```bash
❯   arp-scan -I wlan0 --localnet
Interface: wlan0, type: EN10MB, MAC: 74:97:79:b6:78:b1, IPv4: 192.168.2.101
Starting arp-scan 1.10.0 with 256 hosts (https://github.com/royhills/arp-scan)
192.168.2.1	1c:a0:d3:62:16:88	Intertecno SRL "NISUTA"

1 packets received by filter, 0 packets dropped by kernel
Ending arp-scan 1.10.0: 256 hosts scanned in 2.027 seconds (126.30 hosts/sec). 1 responded
❯   arp-scan -I wlan0 --localnet --ignoredups
Interface: wlan0, type: EN10MB, MAC: 74:97:79:b6:78:b1, IPv4: 192.168.2.101
Starting arp-scan 1.10.0 with 256 hosts (https://github.com/royhills/arp-scan)
192.168.2.1	1c:a0:d3:62:16:88	Intertecno SRL "NISUTA"
192.168.2.105	9a:f1:10:a6:c8:2c	(Unknown: locally administered)
192.168.2.104	2e:44:0d:e7:4c:e5	(Unknown: locally administered)
192.168.2.106	2e:fe:4d:b2:80:ac	(Unknown: locally administered)
192.168.2.108	f2:82:42:30:f6:65	(Unknown: locally administered)

5 packets received by filter, 0 packets dropped by kernel
Ending arp-scan 1.10.0: 256 hosts scanned in 2.015 seconds (127.05 hosts/sec). 5 responded
```

Considerar escanear el CIDR  198.168.0.0/16 por mas que tu mascara de red sea 255.255.255.0 porque en ocasiones descubre mas equipos ya que el cliente piensa que tiene segmentada la red pero en realidad no

Alternativa manual en caso de que con nmap o arp-scan no encontrar ips conetadas ( host activos ):
``` bash
  1  #!/bin/bash
  2 function ctrl_c(){
  3     echo -e "\n\n[!] Saliendo..."
  4     tput cnorm; exit 1
  5 }
  6 
  7 tput civis
  8 
  9 #Ctrl + c
 10 trap ctrl_c SIGINT
 11 
 12 #CODE
 13 for i in $(seq 1 254); do
 14     timeout 1 bash -c "ping -c 1 192.168.2.$i" &>/dev/null && echo "[+] Host 192.168.2.$i - ACTIVE" &
 15 done
 16 
 17 wait
 18 
 19 tput cnorm
```

# Nota! NO usar!  deja sin internet, deben ser muchos paquetes

nmap puede llegar a escanear unos 1000 host por minuto y es importante conocer otra herramienta que puede llegar a escanear unos millones por minuto la cual es **masscan** 
```shell 
❯ masscan -p21,22,139,445,8080,80,443 -Pn 192.168.0./16 --rate=10000
Starting masscan 1.3.2 (http://bit.ly/14GZzcT) at 2024-01-10 23:28:41 GMT
Initiating SYN Stealth Scan
Scanning 65536 hosts [7 ports/host]
Discovered open port 8080/tcp on 192.168.2.117
```