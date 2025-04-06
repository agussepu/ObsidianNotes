---
tags:
  - Reconocimiento
aliases:
  - scripts en lua
---
---
Nmap permite a los profesionales de seguridad personalizar y extender sus capacidades mediante la creación de scripts personalizados en el lenguaje de programación **Lua**. Lua es un lenguaje de scripting simple, flexible y poderoso que es fácil de aprender y de usar para cualquier persona interesada en crear scripts personalizados para Nmap.

Para utilizar Lua como un script personalizado en Nmap, es necesario tener conocimientos básicos del lenguaje de programación Lua y comprender la estructura básica que debe tener el script. La estructura básica de un script de Lua en Nmap incluye la definición de una tabla, que contiene diferentes campos y valores que describen la funcionalidad del script.

Los campos más comunes que se definen en la tabla de un script de Lua en Nmap incluyen:

- **description**: Este campo se utiliza para proporcionar una descripción corta del script y su funcionalidad.
- **categories**: Este campo se utiliza para especificar las categorías a las que pertenece el script, como descubrimiento, explotación, enumeración, etc.
- **author**: Este campo se utiliza para identificar al autor del script.
- **license**: Este campo se utiliza para especificar los términos de la licencia bajo la cual se distribuye el script.
- **dependencies**: Este campo se utiliza para especificar cualquier dependencia de biblioteca o software que requiera el script para funcionar correctamente.
- **actions**: Este campo se utiliza para definir la funcionalidad específica del script, como la realización de un escaneo de puertos, la detección de vulnerabilidades, etc.

Una vez que se ha creado un script de Lua personalizado en Nmap, se puede invocar utilizando el parámetro **–script** y el nombre del archivo del script. Con la creación de scripts personalizados en Lua, es posible personalizar aún más las capacidades de Nmap y obtener información valiosa sobre los sistemas y servicios en la red.

script a modo de ejemplo:
```lua
 1 -- HEAD --
  2 
  3 description = [[
  4 Script de ejemplo que enumera y reporta puertos abiertos por TCP
  5 ]]
  6 
  7 -- RULE --
  8 
  9 portrule = function(host, port)
 10     return port.protocol == "tcp"
 11         and port.state == "open"
 12 end
 13 
 14 -- ACTION --
 15 
 16 action = function(host, port)
 17     return "This port is open"
 18 end
 19
 ```

ejecutamos el script que creamos:
 ```bash
❯ nmap --script /home/agus/Documentos/Academia/IntroHacking/example.nse -p22 192.168.2.101
Starting Nmap 7.94 ( https://nmap.org ) at 2024-01-09 18:33 -03
Nmap scan report for agus-82yu (192.168.2.101)
Host is up (0.000079s latency).

PORT   STATE SERVICE
22/tcp open  ssh
|_example: This port is open

Nmap done: 1 IP address (1 host up) scanned in 0.16 seconds
 ```