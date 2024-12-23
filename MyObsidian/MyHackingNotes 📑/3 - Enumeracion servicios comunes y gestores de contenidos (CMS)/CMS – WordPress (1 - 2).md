En esta clase estaremos enseñando técnicas de enumeración para el gestor de contenido (**CMS**) **WordPress**. Un gestor de contenido es una herramienta que permite la creación, gestión y publicación de contenidos digitales en la web, como por ejemplo páginas web, blogs, tiendas en línea, entre otros.

WordPress es un CMS de código abierto muy popular que fue lanzado en 2003. Es utilizado por millones de sitios web en todo el mundo y se destaca por su facilidad de uso y flexibilidad. Con WordPress, los usuarios pueden crear y personalizar sitios web sin necesidad de conocimientos de programación avanzados. Además, cuenta con una amplia variedad de plantillas y plugins que permiten añadir funcionalidades adicionales al sitio.

El proyecto que utilizamos en esta clase para enumerar un WordPress es el siguiente:

- **DVWP**: [https://github.com/vavkamil/dvwp](https://github.com/vavkamil/dvwp)

Tenemos que tener en cuenta que este contendor crea volumenes y a la hora de finalizar su uso debemos de borrarlo

```bash
#vemos los volumenes de docker existentes
docker volume ls 

docker volume rm $(docker volumes ls -q)
#borrar voluemenes
```


la herramienta de consola de la pagina de exploitdb es searchsploit en este caso la usaremos para buscar vulnerabilidades que nos permitan enumerar usuarios validos para wordpress

```bash
❯ searchsploit wordpress user enumeration
------------------------------------------------------------------------------------------------------------------------------------------------------ ---------------------------------
 Exploit Title                                                                                                                                        |  Path
------------------------------------------------------------------------------------------------------------------------------------------------------ ---------------------------------
WordPress Core < 4.7.1 - Username Enumeration                                                                                                         | php/webapps/41497.php
------------------------------------------------------------------------------------------------------------------------------------------------------ ---------------------------------
Shellcodes: No Results
```

sabiendo la vulnerabilidad que debe ser menor a 4.7.1 con `whatweb` podemos ver la version de la pagina de wordpress

Una de las herramientas que utilizamos en esta clase para enumerar este gestor de contenido es **Wpscan**. Wpscan es una herramienta de código abierto que se utiliza para escanear sitios web en busca de vulnerabilidades de seguridad en WordPress.

Con Wpscan, podemos realizar una enumeración completa del sitio web y obtener información detallada sobre la instalación de WordPress, como la versión utilizada, los plugins y temas instalados y los usuarios registrados en el sitio. También nos permite realizar pruebas de fuerza bruta para descubrir contraseñas débiles y vulnerabilidades conocidas en plugins y temas.

Wpscan es una herramienta muy útil para los administradores de sitios web que desean mejorar la seguridad de su sitio WordPress, ya que permite identificar y corregir vulnerabilidades antes de que sean explotadas por atacantes malintencionados. Además, es una herramienta fácil de usar y muy efectiva para identificar posibles debilidades de seguridad en nuestro sitio web.

El uso de esta herramienta es bastante sencillo, a continuación se indica la sintaxis básica:

➜ `wpscan --url https://example.com`

Si deseas enumerar usuarios o plugins vulnerables en WordPress utilizando la herramienta wpscan, puedes añadir los siguientes parámetros a la línea de comandos:

**➜** `wpscan --url https://example.com --enumerate u`

En caso de querer enumerar plugins existentes los cuales sean vulnerables, puedes añadir el siguiente parámetro a la línea de comandos:

➜ `wpscan --url https://example.com --enumerate vp`

En caso de querer q nos muestre la vulnerabilidades necesitamos jugar con el api token el cual conseguiremos registrandonos en la pagina web de wpscan

➜ `wpscan --url https://example.com --enumerate vp --api-token=shsodfho231`


para saber si tenemos capacidad de directory listing debemos en la pagina de wordpres poner `https://127.0.0.1/..../wp-content/plugins` en caso de estar vulnerable veremos en esta parte de la pagina los direcctorios y plugins existentes

En el codigo fuente a veces se pueden llegar a ver plugins por lo que podemos hacer..
`curl -s -X GET https://127.0.0.1/wordpress/` y luego grepearlo con una expresion regular para que me muestre dichos plugins `.. | grep -oP 'plugins/\K.*'` o `.. | grep -oP 'plugins/\K[^/]+' | sort -u`


Asimismo, otro de los recursos que contemplamos en esta clase es el archivo **xmlrpc.php**. Este archivo es una característica de WordPress que permite la comunicación entre el sitio web y aplicaciones externas utilizando el protocolo **XML-RPC**.

El archivo xmlrpc.php es utilizado por muchos plugins y aplicaciones móviles de WordPress para interactuar con el sitio web y realizar diversas tareas, como publicar contenido, actualizar el sitio y obtener información.

Sin embargo, este archivo también puede ser abusado por atacantes malintencionados para aplicar **fuerza bruta** y descubrir **credenciales válidas** de los usuarios del sitio. Esto se debe a que xmlrpc.php permite a los atacantes realizar un número ilimitado de solicitudes de inicio de sesión sin ser bloqueados, lo que hace que la ejecución de un ataque de fuerza bruta sea relativamente sencilla.

Y esto lo vemos de la siguiente manera ponemos `http://.../xmlrpc.php`y debería saltarnos una pagina que diga `XML-RPC server acepts POST requests only` luego debemos tramitar una petición por post a esa pagina

`curl -s -X POST https://127.0.0.1/wordpress/xmlrpc.php` Esto nos dirá que no esta bien tramitada la petición por post y por lo tanto ahora debemos tramitar una petición por post que nos permita listar los métodos y se hace de la siguiente manera:

Post Request:
https://nitesculucian.github.io/2019/07/01/exploiting-the-xmlrpc-php-on-all-wordpress-versions/
```php
POST /xmlrpc.php HTTP/1.1
Host: example.com
Content-Length: 135

<?xml version="1.0" encoding="utf-8"?> 
<methodCall> 
<methodName>system.listMethods</methodName> 
<params></params> 
</methodCall>
```

Esto lo ponemos en un archivo con extension .xml

y para adjuntar ese archivo a la peticion post lo hacemos de la siguiente manera con el parametro `-d@`

`curl -s -X POST https://127.0.0.1/wordpress/xmlrpc.php -d@file.xml`

y de aca nos vas a responder el servidor con todos los metodos disponibles y nosotros debemos buscar entre ellos a ver si se encuentra este --> `<value><string>wp.getUsersBlogs</string></value>`

y con este archivo nos permite hacer un ataque de fuerza bruta ya que nosotro conocemos el usuario debido a que nos los muestra en el wordpress solo nos falta la contraseña

La siguiente solicitud representa el ataque de fuerza bruta más común:
```xml
POST /xmlrpc.php HTTP/1.1
Host: example.com
Content-Length: 235

<?xml version="1.0" encoding="UTF-8"?>
<methodCall> 
<methodName>wp.getUsersBlogs</methodName> 
<params> 
<param><value>s4vitar</value></param> 
<param><value>\{\{your password\}\}</value></param> 
</params> 
</methodCall>
```
...

---

En esta clase, veremos cómo abusar del archivo **xmlrpc.php** para mediante la creación de un script de Bash aplicar fuerza bruta. El objetivo de este ejercicio será demostrar cómo los atacantes pueden utilizar este archivo existente en WordPress para intentar descubrir credenciales válidas y comprometer la seguridad del sitio web.

Para lograrlo, crearemos un script de Bash en el cual emplearemos la herramienta cURL para enviar solicitudes XML-RPC al archivo xmlrpc.php del sitio web WordPress. A través del método **wp.getUsersBlogs**, enviaremos una estructura XML que contendrá el nombre de usuario y la contraseña a probar.

En caso de que las credenciales no sean correctas, el servidor responderá con un mensaje de error que indica que las credenciales son incorrectas. Sin embargo, si las credenciales son válidas, la respuesta del servidor será diferente y no incluirá el mensaje de error.

De esta forma, podremos utilizar la respuesta del servidor para determinar cuándo hemos encontrado credenciales válidas y, de esta forma, tener acceso al sitio web de WordPress comprometido.

Cabe destacar que el método wp.getUsersBlogs **no es el único método existente**, ni mucho menos la única vulnerabilidad en xmlrpc.php. Existen otros métodos como **wp.getUsers**, **wp.getAuthors** o **wp.getComments**, entre otros, que también pueden ser utilizados por atacantes para realizar ataques de fuerza bruta y comprometer la seguridad del sitio web de WordPress.

Por lo tanto, es importante tener en cuenta que la seguridad de un sitio web de WordPress no solo depende de tener contraseñas seguras y actualizadas, sino también de estar atentos a posibles vulnerabilidades en el archivo xmlrpc.php y otras áreas del sitio web.

![[xml_brut_force.png]]

en este script hacemos fuerza bruta al usuario s4vitar mediante un diccionario llamado rockyou

Esto mismo puede hacerse con wpscan de una manera un poco mas rapida y optimizada
![[wpscan_image.png]]

Teniendo la contraseña en el panel `/wp-admin` podemos autenticarnos