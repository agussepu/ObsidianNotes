---
aliases:
  - Google dork
tags:
  - Reconocimiento
---
---
*NOTA: con la herramienta exiftool podemos ver metadatos de un archivo (ver si es solo pdf)*

*NOTA: https://www.exploit-db.com/ lugar donde hay vulnerabilidades con el código* ademas de haber dorks de google hacking

El ‘**Google Dork**‘ es una técnica de búsqueda avanzada que utiliza operadores y palabras clave específicas en el buscador de Google para encontrar información que normalmente no aparece en los resultados de búsqueda regulares.

La técnica de ‘**Google Dorking**‘ se utiliza a menudo en el hacking para encontrar información sensible y crítica en línea. Es una forma eficaz de recopilar información valiosa de una organización o individuo que puede ser utilizada para realizar pruebas de penetración y otros fines de seguridad.

Al utilizar Google Dorks, un atacante puede buscar información como nombres de usuarios y contraseñas, archivos confidenciales, información de bases de datos, números de tarjetas de crédito y otra información crítica. También pueden utilizar esta técnica para identificar vulnerabilidades en aplicaciones web, sitios web y otros sistemas en línea.

Es importante tener en cuenta que la técnica de Google Dorking **no es ilegal en sí misma**, pero puede ser utilizada con fines maliciosos. Por lo tanto, es crucial utilizar esta técnica con responsabilidad y ética en el contexto de la seguridad informática y el hacking ético.

Recordemos que desde la web de pentest tools podemos usar el google hacking y usar los 18 dorks mas usados 

Dorks mas comunes:

***site*** buscara unicamente el dominio y resultados debajo del mismo pero solamente involucra el dominio que busquemos7
site:tinder 
```python
site:tinder 
```

***filetype*** unicamente muestra recursos del tipo que busquemos
```python
site:tinder filetype:txt
```

***intext*** busca archivos que en el texto de entrada este lo que pusimos
```python
intext:tinder.com filetype:pdf
```

