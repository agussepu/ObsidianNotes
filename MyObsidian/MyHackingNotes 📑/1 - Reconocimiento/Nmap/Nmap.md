---
tags:
  - Reconocimiento
  - HackingTools
aliases:
  - nmap
---
**Nmap** es una herramienta de **escaneo de red** gratuita y de código abierto que se utiliza en pruebas de penetración (pentesting) para explorar y auditar redes y sistemas informáticos.

Con Nmap, los profesionales de seguridad pueden identificar los **hosts** conectados a una red, los **servicios** que se están ejecutando en ellos y las **vulnerabilidades** que podrían ser explotadas por un atacante. La herramienta es capaz de detectar una amplia gama de dispositivos, incluyendo enrutadores, servidores web, impresoras, cámaras IP, sistemas operativos y otros dispositivos conectados a una red.
# Uso de nmap
recordar que un puerto puede estar en diferentes **estados**:
- **abierto**
- **cerrado**
- **filtrado**: la herramienta no distingue si esta abierto o cerrado dicho puerto

Al usar nmap debemos indicar que ip vamos a escanear. En total existen *65535* puertos 

**Parametros**:  
1. Enumeramos los **puertos** que queremos con el parámetro -p:
	- -p1-65535: indicamos que queremos enumerar todos los puertos aunque tambien podemos usar -p- en este caso
```bash 
nmap -p- 192.168.2.1
Starting Nmap 7.94 ( https://nmap.org ) at 2024-01-08 17:07 -03
Nmap scan report for _gateway (192.168.2.1)
Host is up (0.0046s latency).
Not shown: 65533 closed tcp ports (reset)
PORT     STATE SERVICE
80/tcp   open  http
1980/tcp open  pearldoc-xact
MAC Address: 1C:A0:D3:62:16:88 (Intertecno SRL Nisuta)

Nmap done: 1 IP address (1 host up) scanned in 33.37 seconds
```

2.  Podemos escanear los puertos mas comunes usando **--top-ports 500** (o los 100 mas comunes depende el numero que le indiquemos)
3. Escanemos únicamente aquellos puertos que están abiertos con el parámetro
**--open**
```bash
❯ nmap --top-ports 500 --open 192.168.2.1
Starting Nmap 7.94 ( https://nmap.org ) at 2024-01-08 17:17 -03
Nmap scan report for _gateway (192.168.2.1)
Host is up (0.0055s latency).
Not shown: 499 closed tcp ports (reset)
PORT   STATE SERVICE
80/tcp open  http
MAC Address: 1C:A0:D3:62:16:88 (Intertecno SRL Nisuta)

Nmap done: 1 IP address (1 host up) scanned in 8.35 seconds
```

4. el parámetro ***-v*** (verbose) no dará mas info a medida que se realice el escaneo dando la posibilidad de hacer enter y ver mas info

5. mediante el parametro ***-n*** podemos quitar la resolución dns para ir mas rápido

6. para que el escaneo vaya mas rápido podemos usar el parametro -T5 (del 0 al 5 podemos usar siendo 0 muy lento y 5 muy rápido)

7. **tcp conect scan** lo usamos con el parametro ***-sT*** se utiliza el  **[[Three-Way Handshake|Three-Way Handshake]]**
	- Nosotros enviamos un SYN y si un puerto esta cerrado nos devolverá un --> RST (Cerrado)
	- SI esta abierto nos devolverá un SYN/ACK para luego devolver un ACK que seria established (conexión establecida) 
	
Para ver las trazas nos pondremos en escucha con:
```bash
❯ sudo tcpdump -iwlan0 -w Captura.cap -v  
tcpdump: listening on wlan0, link-type EN10MB (Ethernet), snapshot length 262144 bytes
```
 y ejecutaremos la traza de nmap:
 ```bash
 ❯ nmap -p80 -sT 192.168.2.1
 ```
y finalmente abriamos el archivo tcpdump con wireshark para ver dichas trazas
 ```bash
 wireshark Captura.cap &>/dev/null & disown  
 ```


8. El parametro ***-Pn*** se recomiendo usarlo para que de por hecho que el host esta activo

9. con el parametro ***-sU*** podemos escanear por el protocolo UDP el cual sera un poco mas lento el escaneo
 ```bash
❯ nmap --top-ports 500 -sU 192.168.2.1 -n -v -Pn
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower.
Starting Nmap 7.94 ( https://nmap.org ) at 2024-01-08 18:12 -03
Initiating ARP Ping Scan at 18:12
Scanning 192.168.2.1 [1 port]
Completed ARP Ping Scan at 18:12, 0.09s elapsed (1 total hosts)
Initiating UDP Scan at 18:12
Scanning 192.168.2.1 [500 ports]
Discovered open port 1900/udp on 192.168.2.1
Discovered open port 53/udp on 192.168.2.1
Completed UDP Scan at 18:12, 2.54s elapsed (500 total ports)
Nmap scan report for 192.168.2.1
Host is up (0.011s latency).
Not shown: 494 closed udp ports (port-unreach)
PORT     STATE         SERVICE
53/udp   open          domain
67/udp   open|filtered dhcps
123/udp  open|filtered ntp
1026/udp open|filtered win-rpc
1027/udp open|filtered unknown
1900/udp open          upnp
MAC Address: 1C:A0:D3:62:16:88 (Intertecno SRL Nisuta)

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 2.76 seconds
           Raw packets sent: 609 (30.824KB) | Rcvd: 546 (32.441KB)
```

10. Con el parametro ***-O*** podemos ver que sistemas operativos tiene el target que escaneamos (no se recomienda)
```bash 
❯ nmap -O 192.168.2.101
```

11. Para ver que dispositivos hay en nuestra red podemos usar:
``` bash
❯ arp-scan -I wlan0 --localnet
❯ nmap -sn 192.168.2.0/24 | grep -oP '\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}'
```

12. Al saber que puertos hay abierto podemos usar -sV para tener mas informacion de cada puerto
``` bash
nmap -p80,1980 -sV 192.168.2.1 -n -v -Pn
```