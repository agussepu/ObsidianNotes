# 1. Subdomain enumeration

***Spyhunt***: 
	 *Usage:* 
	 Esto nos devolverá todos los subdominios existentes (incluso los inactivos)
	 1. `python3 spyhunt.py -s spotify.com --save spotifysubs`
	 Guardamos solo los subdominios activos
	 2. `python3 spyhunt.py --probe spotifysubs --save good_spotify_subs`
	
---
# 2. Content Discovery
Una vez listados todos los subdominios hay que empezar con el *reconocimiento activo* a cada subdominio encontrado. Una buena practica es verificar las IPs de cada subdominio ya que si varios subdominios comparten la misma IP puedes escanear esa sola IP

Dirsearch
Gobuster
OWASP ZAP (spider)
ffuf
spyhunt
wffuf

---
# 3. Technology Discovery
wappalyzer
whatweb

---
# 4. Wayback URLS
Wayback Machine (https:// archive.org/web/),

---
# 5. Port and services Scanning

shodan

---
# Recursos
Guia de BugBounty: https://www.youtube.com/watch?v=L-qSSZIP3rU&t=2109s

Libro "Bug bounty Bootcamp": file:///home/agus/Documentos/Books/Bug%20Bounty%20Bootcamp%20The%20Guide%20to%20Finding%20and%20Reporting%20Web%20Vulnerabilities%20by%20Vickie%20Li.pdf