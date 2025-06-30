**Todas la computadoras** del mundo **tienen una dirección** para poder enviar packets. Aunque algunas solo reciben paquetes de cierto tipo y otras reciben solo packets de cierto tipo, de cierto tipo de computadoras. A continuación **nos centraremos solo en la data** enviada en los paquetes (HTTP mensajes) mas no en los paquetes en si.


# What Happens When You Visit a Website
### Step 1: Extracting the Domain Name
Cuando ingresas una URL como `http://www.google.com/` en tu navegador, lo primero que hace el navegador es **extraer el nombre de dominio** de esa URL. Ese dominio es **la parte que identifica a qué sitio web querés acceder**. Es simplemente una dirección legible por humanos que apunta a un servidor en internet
- Este nombre no es al azar: **tiene que seguir ciertas reglas**, que están definidas en documentos llamados **RFCs** (Request For Comments)

### Step 2: Resolving an IP Address
Tras determinar el nombre de dominio, su navegador utiliza IP para buscar la dirección IP asociada al dominio. Existen dos tipos de IP -> IPv4 y IPv6
Para encontrar la dirección IP a la que pertenece el dominio nuestro navegador hace una consulta a un Domain Name Server ([[DNS]])

### Step 3: Establishing a TCP Connection
Una vez que ya sabes la IP del servidor (gracias al DNS), **tu computadora necesita hablar con ese servidor**, y para eso utiliza el protocolo **TCP (Transmission Control Protocol)**
Cuando escribís `http://www.google.com` en tu navegador, se siguen estos pasos:

1. **Se resuelve el dominio**: se convierte `www.google.com` en una IP (ej. `216.58.201.228`).
2. **Se abre una conexión TCP** con esa IP, en el **puerto 80** (porque estás usando **HTTP**).
3. **Encima de esa conexión TCP**, se envía una **petición HTTP** (por ejemplo: “dame la página de inicio”).
4. El servidor responde también con HTTP, **usando la misma conexión TCP**.

### Step 4: Sending an HTTP Request 
### Step 5: Server Response
Si la conexión en el paso 3 tiene éxito, su navegador debería preparar y enviar una petición HTTP y recibir una respuesta HTTP. Un **dato importante** es que mas allá de los estandartes de los **status code** en la response **no existe una aplicación estricta** de los mismos por lo que podemos ver servidores que devuelven un 200 pero con un error en el body.

![[httpStatusCodes.png]]

### Step 6: Rendering the Response

