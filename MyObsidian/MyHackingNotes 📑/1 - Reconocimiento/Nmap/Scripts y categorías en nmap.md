---
tags:
  - Reconocimiento
aliases:
  - scripts nmap
---

Una de las características más poderosas de **Nmap** es su capacidad para automatizar tareas utilizando **scripts personalizados**. Los scripts de Nmap permiten a los profesionales de seguridad automatizar las tareas de reconocimiento y descubrimiento en la red, además de obtener información valiosa sobre los sistemas y servicios que se están ejecutando en ellos. El parámetro **–script** de Nmap permite al usuario seleccionar un conjunto de scripts para ejecutar en un objetivo de escaneo específico.

Existen diferentes categorías de scripts disponibles en Nmap, cada una diseñada para realizar una tarea específica. Algunas de las categorías más comunes incluyen:

- **default**: Esta es la categoría predeterminada en Nmap, que incluye una gran cantidad de scripts de reconocimiento básicos y útiles para la mayoría de los escaneos.
- **discovery**: Esta categoría se enfoca en descubrir información sobre la red, como la detección de hosts y dispositivos activos, y la resolución de nombres de dominio.
- **safe**: Esta categoría incluye scripts que son considerados seguros y que no realizan actividades invasivas que puedan desencadenar una alerta de seguridad en la red.
- **intrusive**: Esta categoría incluye scripts más invasivos que pueden ser detectados fácilmente por un sistema de detección de intrusos o un Firewall, pero que pueden proporcionar información valiosa sobre vulnerabilidades y debilidades en la red.
- **vuln**: Esta categoría se enfoca específicamente en la detección de vulnerabilidades y debilidades en los sistemas y servicios que se están ejecutando en la red.

En conclusión, el uso de scripts y categorías en Nmap es una forma efectiva de automatizar tareas de reconocimiento y descubrimiento en la red. El parámetro **–script** permite al usuario seleccionar un conjunto de scripts personalizados para ejecutar en un objetivo de escaneo específico, mientras que las diferentes categorías disponibles en Nmap se enfocan en realizar tareas específicas para obtener información valiosa sobre la red.

Con -sCV nos tira un conjunto de scripts mas populares este es la unión de -sV que nos muestra la versión y el servicio y -sC que son el conjunto de scripts:
```bash
sudo nmap -p- 192.168.2.1 -sCV
```

Cada script tiene un conjunto de categorias por lo que cada uno puede estar dentro de una o varias categorias la cuales son:
```bash
❯ locate .nse | xargs grep "categories" | grep -oP '".*?"' | sort -u
"auth"
"broadcast"
"brute"
"default"
"discovery"
"dos"
"exploit"
"external"
"fuzzer"
"intrusive"
"malware"
"safe"
"version"
"vuln"
```

en caso de querer ejecutar un script especifico lo podemos hacer con --script aunque también podemos ejecutar categorías de scripts:
```bash
#En este caso solo ejecutamos scripts pertenecientes a la categoria vuln and safe
nmap -p22 192.168.2.101 --script="vuln and safe"
```

-------
Montamos con python3 un servidor http 
```bash
❯ python3 -m http.server 80
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...
```
Verificamos que servicio corre por el puerto 80:
```bash
❯ lsof -i:80
COMMAND    PID USER FD   TYPE DEVICE SIZE/OFF NODE NAME
python3 149850 root 3u  IPv4 539901      0t0  TCP *:http (LISTEN)
```
Vemos mediante el PID en que ruta del sistema esta montado el servidor
```bash
❯ pwdx 149850
149850: /home/agus/Documentos/Academia/IntroHacking/Admin
```
una vez montado el servidor web temporal buscaremos directorios dentro de el..
lanzamos un reconocimiento al puerto 80 buscando directorios con el **--script http-enum** 

Este script es un fuzzing lo que hace es hacer fuerza bruta buscando directorios comunes
```bash
❯ nmap -p80 192.168.2.101 --script http-enum
Starting Nmap 7.94 ( https://nmap.org ) at 2024-01-09 17:52 -03
Nmap scan report for agus-82yu (192.168.2.101)
Host is up (0.000062s latency).

PORT   STATE SERVICE
80/tcp open  http
| http-enum: 
|_  /Admin/: Possible admin folder

Nmap done: 1 IP address (1 host up) scanned in 9.28 seconds
```

Ahora haremos lo mismo pero vamos a interceptar con tcpdump el reconocimiento  (lo loopback)
```bash
tcpdump -i lo -w Captura.cap -v 
```

y abrimos el archivo captura.cap con tshark (se recomienda enviar los stderr al dev null)
``` bash
tshark -r Captura.cap 2>/dev/null 
```
contamos la cantidad de directorios que tiene el diccionario de fuerza bruta de el script q utilizamos anteriormente desde el archivo que abrimos con tshark
``` bash
❯ tshark -r Captura.cap -Y "http" -Tfields -e tcp.payload 2>/dev/null | xxd -ps -r | grep "GET" | awk '{print $2}' | wc -l
1112
``` 

Ver todos los scripts que tiene nmap
``` bash
locate .nse 
``` 
