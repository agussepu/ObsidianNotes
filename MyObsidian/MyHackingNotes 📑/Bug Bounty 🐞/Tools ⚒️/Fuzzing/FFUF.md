---
tags:
  - HackingTools
---
---
```bash
#Con -p reletizamos las peticiones a 2 segundos por cada una y con -fc ocultamos aquellas con codigo de error 403 

ffuf -w /usr/share/SecLists/Discovery/WebContent/common.txt -u http://<domain>/FUZZ -fc 403 -p 2
```
