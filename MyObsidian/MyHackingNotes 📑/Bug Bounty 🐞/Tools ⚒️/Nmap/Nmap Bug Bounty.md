---
tags:
  - Reconocimiento
  - HackingTools
aliases:
  - Nmap Bug Bounty
---
---
A la hora de hacer un escaneo en bug bounty debemos ir un poco mas lento que un CTF

```shell 
# -A: Enable OS detection, version detection, script scanning, and traceroute
# Con -F escanea solo los primeros 100 puertos mas comunes y -T1 es la plantilla de velocidad

nmap -A -F -T1 <ip-address> -v
```

Ryan John recomienda escanear solo estos puertos si estamos en un programa de bug bounty para no golpear todos los puertos (65536)
![[Pasted image 20250315221003.png]]

