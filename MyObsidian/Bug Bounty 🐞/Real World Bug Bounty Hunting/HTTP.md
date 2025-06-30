## Request Methods

### GET
- Recupera información de una URI (o URL).
- **No debe modificar datos**, solo leerlos.
- Se usa al visitar cualquier enlace o página.

### HEAD
- Igual que GET, pero **no devuelve el cuerpo** de la respuesta.
- Se usa para obtener solo las cabeceras.

### POST

- Ejecuta una **acción en el servidor** (crear, enviar, registrar, etc.).
- Ej: publicar un comentario o registrarse.    

### PUT
- Actualiza un recurso **existente** en el servidor.
- Ej: modificar un post o cuenta ya creada.

### DELETE
- Pide eliminar un recurso del servidor.

### TRACE
- Refleja la solicitud de vuelta al cliente.
- Sirve para **pruebas y diagnóstico**.

### CONNECT
- Se usa con **proxies** para iniciar una comunicación bidireccional.
- Ej: acceder a sitios HTTPS a través de un proxy.
### OPTIONS
- Informa qué métodos HTTP acepta el servidor (GET, POST, PUT…).
- Usado por los navegadores como **preflight** para peticiones especiales (ej. con `application/json`)
- Ayuda a prevenir **CSRF**.

### Nota extra

- **URI** = identificador de recurso (ej: `/archivo.txt`)
    
- **URL** = URI que incluye cómo ubicar el recurso en la red (ej: `http://sitio.com/archivo.txt`)
    
- En el texto se usa “URL” aunque técnicamente se refieren a cualquier URI.


## HTTP Is Stateless (no tiene estado)
Cuando se dice que **HTTP es un protocolo sin estado (stateless)**, significa que **cada solicitud HTTP que hace un cliente (como tu navegador) al servidor es completamente independiente de las anteriores**. El servidor **no recuerda nada** sobre las solicitudes previas realizadas por ese mismo cliente

*Para aclarar este confuso concepto*, considera este ejemplo: si tú y yo mantuviéramos una conversación sin estado, antes de cada frase pronunciada yo tendría que empezar con «Soy Peter Yaworski; estábamos hablando de hacking». Entonces tendrías que recargar toda la información sobre lo que estábamos discutiendo sobre piratería informática. Piensa en lo que Adam Sandler hace por Drew Barrymore cada mañana en 50 First Dates (si no has visto la película, deberías hacerlo).

**Para evitar tener que reenviar su nombre de usuario y contraseña** en cada petición HTTP, **los sitios web utilizan cookies** o autenticación básica.