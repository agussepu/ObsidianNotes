---
aliases:
  - enumeracion de subdominios
tags:
  - Reconocimiento
---
--- 
La enumeración de **subdominios** es una de las fases cruciales en la seguridad informática para identificar los subdominios asociados a un dominio principal.

Los subdominios son parte de un dominio más grande y a menudo están configurados para apuntar a diferentes recursos de la red, como servidores web, servidores de correo electrónico, sistemas de bases de datos, sistemas de gestión de contenido, entre otros.

Al identificar los subdominios vinculados a un dominio principal, un atacante podría obtener información valiosa para cada uno de estos, lo que le podría llevar a encontrar **vectores de ataque potenciales**. Por ejemplo, si se identifica un subdominio que apunta a un servidor web vulnerable, el atacante podría utilizar esta información para intentar explotar la vulnerabilidad y acceder al servidor en cuestión.

Existen diferentes herramientas y técnicas para la enumeración de subdominios, tanto pasivas como activas. Las **herramientas** **pasivas** permiten obtener información sobre los subdominios sin enviar ninguna solicitud a los servidores identificados, mientras que las **herramientas activas** envían solicitudes a los servidores identificados para encontrar subdominios bajo el dominio principal.

Algunas de las **herramientas pasivas** más utilizadas para la enumeración de subdominios incluyen la búsqueda en motores de búsqueda como Google, Bing o Yahoo, y la búsqueda en registros DNS públicos como **PassiveTotal** o **Censys**. Estas herramientas permiten identificar subdominios asociados con un dominio, aunque no siempre son exhaustivas. Además, existen herramientas como **CTFR** que utilizan registros de certificados **SSL/TLS** para encontrar subdominios asociados a un dominio.

También se pueden utilizar páginas online como **Phonebook.cz** e **Intelx.io**, o herramientas como **sublist3r**, para buscar información relacionada con los dominios, incluyendo subdominios.

Por otro lado, las **herramientas activas** para la enumeración de subdominios incluyen herramientas de fuzzing como **wfuzz** o **gobuster**. Estas herramientas envían solicitudes a los servidores mediante ataques de fuerza bruta, con el objetivo de encontrar subdominios válidos bajo el dominio principal.

A continuación, os adjuntamos los enlaces a las herramientas vistas en esta clase:

- **Phonebook** (Herramienta pasiva): [https://phonebook.cz/](https://phonebook.cz/)
- **Intelx** (Herramienta pasiva): [https://intelx.io/](https://intelx.io/)
- **CTFR** (Herramienta pasiva): [https://github.com/UnaPibaGeek/ctfr](https://github.com/UnaPibaGeek/ctfr)
- **Gobuster** (Herramienta activa): [https://github.com/OJ/gobuster](https://github.com/OJ/gobuster)
- **Wfuzz** (Herramienta activa): [https://github.com/xmendez/wfuzz](https://github.com/xmendez/wfuzz)
- **Sublist3r** (Herramienta pasiva): [https://github.com/huntergregal/Sublist3r](https://github.com/huntergregal/Sublist3r)

---
**NOTA: en /usr/share/ clone SecLists son diccionarios para fuerza bruta**
# Numeración pasiva:
Nota: no pude usar esta herraminetas pero basicamente hace peticiones aca https://crt.sh/
CTRF esta instalado en /opt se utiliza para buscar subdominios de un dominio
```bash
❯ python3 ctfr.py -d tinder.com

          ____ _____ _____ ____  
         / ___|_   _|  ___|  _ \ 
        | |     | | | |_  | |_) |
        | |___  | | |  _| |  _ < 
         \____| |_| |_|   |_| \_\
	
     Version 1.2 - Hey don't miss AXFR!
    Made by Sheila A. Berta (UnaPibaGeek)
	

[!] ---- TARGET: tinder.com ---- [!] 
```

Sublist3r esta herramienta esta instalda en /opt 
```bash
❯ python3 sublist3r.py -d tinder.com

                 ____        _     _ _     _   _____
                / ___| _   _| |__ | (_)___| |_|___ / _ __
                \___ \| | | | '_ \| | / __| __| |_ \| '__|
                 ___) | |_| | |_) | | \__ \ |_ ___) | |
                |____/ \__,_|_.__/|_|_|___/\__|____/|_|
                
                # Coded By Ahmed Aboul-Ela - @aboul3la

```

#  Numeración activa ( ataque fuerza bruta ):

**gobuster**
```shell
❯ gobuster vhost -u https://tinder.com -w /usr/share/SecLists/Discovery/DNS/subdomains-top1million-5000.txt -t 20 | grep -v "403"
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:             https://tinder.com
[+] Method:          GET
[+] Threads:         20
[+] Wordlist:        /usr/share/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
[+] User Agent:      gobuster/3.6
[+] Timeout:         10s
[+] Append Domain:   false
===============================================================
Starting gobuster in VHOST enumeration mode
===============================================================
Found: www.shop Status: 421 [Size: 1003]
Found: www.admin Status: 421 [Size: 1003]
Progress: 4989 / 4990 (99.98%)
===============================================================
Finished
===============================================================
```


wfuzz (te permite fuzzear muchas cosas como descubrimiento de rutas, parametros, solicitudes por GET,POST, extensiones )
```bash 
❯ wfuzz -c --hc=403 -t 20 -w /usr/share/SecLists/Discovery/DNS/subdomains-top1million-5000.txt -H "Host: FUZZ.tinder.com" http://tinder.com
********************************************************
* Wfuzz 3.1.0 - The Web Fuzzer                         *
********************************************************

Target: http://tinder.com/
Total requests: 4989

=====================================================================
ID           Response   Lines    Word       Chars       Payload                                                                                                                
=====================================================================

000000001:   301        7 L      11 W       167 Ch      "www"                                                                                                                  
000000067:   301        7 L      11 W       167 Ch      "staging"                                                                                                              
000000401:   301        7 L      11 W       167 Ch      "tech"                                                                                                                 
000001681:   301        7 L      11 W       167 Ch      "lite"                                                                                                                 

Total time: 0
Processed Requests: 4989
Filtered Requests: 4985
Requests/sec.: 0
```