---
aliases:
  - Fuzzing
tags:
  - Reconocimiento
---
---
En esta clase, hacemos uso de las herramientas **Wfuzz** y **Gobuster** para aplicar **Fuzzing**. Esta técnica se utiliza para descubrir rutas y recursos ocultos en un servidor web mediante ataques de fuerza bruta. El objetivo es encontrar recursos ocultos que podrían ser utilizados por atacantes malintencionados para obtener acceso no autorizado al servidor.

**Wfuzz** es una herramienta de descubrimiento de contenido y una herramienta de inyección de datos. Básicamente, se utiliza para automatizar los procesos de prueba de vulnerabilidades en aplicaciones web.

```bash
# Recoradar que en wfuzz siempre debemos jugar con la palabra FUZZ en donde queremos fuzzear
wfuzz -c -t 200 -w /usr/share/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt https://miwifi.com/FUZZ
```

En este caso con --hc=404 ocultamos aquellos que nos devuelve un codigo de error 404
```bash
wfuzz -c --hc=404 -t 200 -w /usr/share/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt https://miwifi.com/FUZZ
```

En caso de querer q nos muestre respuestas con un total de lineas usaremos --sl=216 
```bash
wfuzz -c --sl=216 --hc=404 -t 200 -w /usr/share/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt https://miwifi.com/FUZZ
```

Para buscar rutas con extension html usaremos 
```bash
wfuzz -c --hc=404 -t 200 -w /usr/share/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt https://miwifi.com/FUZZ.html
```

Para buscar varias extensiones podemos unar otro payload de tipo list con el parametro -z
```bash
wfuzz -c --hc=404 -t 200 -w /usr/share/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt -z list,html-txt-php https://miwifi.com/FUZZ.FUZ2Z
```

Para enumerar identifiacadores o valores como veremos en este caso donde hay muchos productos y talvez podemos encontrar alguno de prueba o algo interesante

```bash
wfuzz -c -t 200 --hw=5907 -z range,1-20000 'https://www.mi.com/shop/buy/detail?product_id=FUZZ'
```

Permite realizar ataques de fuerza bruta en parámetros y directorios de una aplicación web para identificar recursos existentes. Una de las **ventajas** de Wfuzz es que es altamente personalizable y se puede ajustar a diferentes necesidades de pruebas. Algunas de las **desventajas** de Wfuzz incluyen la necesidad de comprender la sintaxis de sus comandos y que puede ser más lenta en comparación con otras herramientas de descubrimiento de contenido.

Para salir de wfuzz es recomendable hacer `ctrl + c ` y luego haces `ctrl + z` y finalmente matar el proceso con `kill %`

---


Por otro lado, **Gobuster** es una herramienta de descubrimiento de contenido que también se utiliza para buscar archivos y directorios ocultos en una aplicación web ( Esta herramienta esta programada en go por lo que funciona muy bien con sockets y conexiones ). Al igual que Wfuzz, Gobuster se basa en ataques de fuerza bruta para encontrar archivos y directorios ocultos. Una de las principales **ventajas** de Gobuster es su velocidad, ya que es conocida por ser una de las herramientas de descubrimiento de contenido más rápidas. También es fácil de usar y su sintaxis es simple. Sin embargo, una **desventaja** de Gobuster es que puede no ser tan personalizable como Wfuzz.

```bash
# Recordar que esto deja huella en los logs de la pagina a la cual le hacemos reconociemiento
gobuster dir -u https://www.miwifi.com/ -w /usr/share/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt -t 200 --add-slash -b 403,404
``` 

Ademas con el parametro -x podemos hacer fuzzing a nivel de extensiones 
```bash
gobuster dir -u https://www.miwifi.com/ -w /usr/share/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt -t 200 -b 403,404 -x html,php,txt
``` 

con menos -s podemos indicarle que codigo de estado positivo queremos que nos de en este caso vamos a pedir q nos de el 200
```bash
gobuster dir -u https://www.miwifi.com/ -w /usr/share/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt -t 50 -s 200 -b '' -x html,php,txt
``` 


También tenemos una herramienta pasiva la cual se llama **ffuf** y la deje en /opt

```bash
./ffuf -c -t 200 -w /usr/share/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt -u https://www.miwifi.com/FUZZ/--mc=200
```

---

Adicionalmente, otra de las herramientas que examinamos en esta clase, perfecta para la enumeración de recursos disponibles en una plataforma en línea, es **BurpSuite**. BurpSuite es una plataforma que integra características especializadas para realizar pruebas de penetración en aplicaciones web. Una de sus particularidades es la función de **análisis de páginas en línea**, empleada para identificar y enumerar los recursos accesibles en una página web.

BurpSuite cuenta con dos versiones: una **versión gratuita** (**BurpSuite Community Edition**) y una **versión de pago** (**BurpSuite Pofessional**).

### BurpSuite Community Edition

Es la **versión gratuita** de esta plataforma, viene incluida por defecto en el sistema operativo. Su función principal es desempeñar el papel de **proxy HTTP** para la aplicación, facilitando la realización de pruebas de penetración.

Un **proxy HTTP** es un filtro de contenido de alto rendimiento, ampliamente usado en el hacking con el fin de interceptar el tráfico de red. Esto permite analizar, modificar, aceptar o rechazar todas las solicitudes y respuestas de la aplicación que se esté auditando.

Algunas de las ventajas que la versión gratuita ofrecen son:

- **Gratuidad**: La versión Community Edition es gratuita, lo que la convierte en una opción accesible para principiantes y profesionales con presupuestos limitados.
- **Herramientas básicas**: Incluye las herramientas esenciales para realizar pruebas de penetración en aplicaciones web, como el Proxy, el Repeater y el Sequencer.
- **Intercepción y modificación de tráfico**: Permite interceptar y modificar las solicitudes y respuestas HTTP/HTTPS, facilitando la identificación de vulnerabilidades y la exploración de posibles ataques.
- **Facilidad de uso**: La interfaz de usuario de la Community Edition es intuitiva y fácil de utilizar, lo que facilita su adopción por parte de usuarios con diversos niveles de experiencia.
- **Aprendizaje y familiarización**: La versión gratuita permite a los usuarios aprender y familiarizarse con las funcionalidades y técnicas de pruebas de penetración antes de dar el salto a la versión Professional.
- **Comunidad de usuarios**: La versión Community Edition cuenta con una amplia comunidad de usuarios que comparten sus conocimientos y experiencias en foros y blogs, lo que puede ser de gran ayuda para resolver problemas y aprender nuevas técnicas.

A pesar de que la Community Edition no ofrece todas las funcionalidades y ventajas de la versión Professional, sigue siendo una opción valiosa para aquellos que buscan comenzar en el ámbito de las pruebas de penetración o que necesitan realizar análisis de seguridad básicos sin incurrir en costos adicionales.

### BurpSuite Proffesional

BurpSuite Proffessional es la **versión de pago** desarrollada por la empresa **PortSwigger**. Incluye, además del proxy HTTP, algunas herramientas de pentesting web como:

- **Escáner de seguridad automatizado**: Permite identificar vulnerabilidades en aplicaciones web de manera rápida y eficiente, lo que ahorra tiempo y esfuerzo.
- **Integración con otras herramientas**: Puede integrarse con otras soluciones de seguridad y entornos de desarrollo para mejorar la eficacia de las pruebas.
- **Extensibilidad**: A través de su API, BurpSuite Professional permite a los usuarios crear y añadir extensiones personalizadas para adaptarse a necesidades específicas.
- **Actualizaciones frecuentes**: La versión profesional recibe actualizaciones periódicas que incluyen nuevas funcionalidades y mejoras de rendimiento.
- **Soporte técnico**: Los usuarios de BurpSuite Professional tienen acceso a un soporte técnico de calidad para resolver dudas y problemas.
- **Informes personalizables**: La herramienta permite generar informes detallados y personalizados sobre las pruebas de penetración y los resultados obtenidos.
- **Interfaz de usuario intuitiva**: La interfaz de BurpSuite Professional es fácil de utilizar y permite a los profesionales de seguridad trabajar de manera eficiente.
- **Herramientas avanzadas**: Incluye funcionalidades avanzadas, como el módulo de intrusión, el rastreador de vulnerabilidades y el generador de payloads, que facilitan la identificación y explotación de vulnerabilidades en aplicaciones web.

En conclusión, tanto la Community Edition como la versión Professional de BurpSuite ofrecen un conjunto de herramientas útiles y eficientes para realizar pruebas de penetración en aplicaciones web. Sin embargo, la versión Professional brinda ventajas adicionales.

La elección entre ambas versiones dependerá del alcance y las necesidades específicas del proyecto o de la empresa. Si se requiere un conjunto básico de herramientas para pruebas de seguridad ocasionales, la Community Edition podría ser suficiente. No obstante, si se busca una solución más completa y personalizable, con soporte técnico y herramientas avanzadas para un enfoque profesional y exhaustivo, la versión Professional sería la opción más adecuada.