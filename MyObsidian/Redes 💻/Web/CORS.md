Por defecto se tiene en todos los navegadores el SOP el cual no permite peticiones entre orígenes cruzados si o si deben tener mismos orígenes (protocolo, dominio, puerto). En caso de necesitar en el desarrollo de manera valida un recurso de origen cruzado o el acceso a un subdomino el SOP por defecto no lo permitira por lo que necesitamos configurar un CORS para que eso pueda hacerse

*CORS* no es un control de acceso de servidor, sino un mecanismo de **confianza declarada** que implementan los navegadores para reforzar la Same‑Origin Policy. Las vulnerabilidades nacen de configuraciones demasiado permisivas o de reflejar sin validar el encabezado `Origin`. Si aseguras correctamente tu whitelist, restringes métodos y cabeceras, y desactivas credenciales cuando no las necesites, podrás exponer APIs a orígenes cruzados de forma segura.

![[CORS_Attack.png]]

Hay que tener cuidado con que el servidor acepte `Access-Control-Allow-Origin: null ` ya que permite la carga de archivos locales


---
El navegador por sí solo te protege contra `* + credentials`, pero **los servidores mal configurados** que reflejan el Origin sin validación **deshabilitan esa protección**. Ahí es donde debes poner atención.

1. **Tu página maliciosa en `evil.com` hace la petición**  
    Desde el JavaScript de `https://evil.com` ejecutas algo como:
    
    ```js
    fetch('https://api.victima.com/datos', {
      credentials: 'include'   // le dice al navegador: “mándame también las cookies”
    })
    ```
    
    El navegador construye la petición y añade la cabecera Origin:
    
    ```
    GET /datos HTTP/1.1
    Host: api.victima.com
    Origin: https://evil.com
    Cookie: sesión=abc123   ← las cookies de api.victima.com para el usuario
    ```
    
2. **El servidor “refleja” el Origin sin validar**  
    En lugar de comprobar que `evil.com` está en su lista blanca, el servidor hace esto:
    
    ```
    Access-Control-Allow-Origin: https://evil.com
    Access-Control-Allow-Credentials: true
    ```
    
3. **El navegador comprueba las cabeceras de la respuesta**  
    Según la especificación CORS, para una petición con `credentials: 'include'` el navegador exige:
    
    - Que `Access-Control-Allow-Credentials` esté puesto en `true`.
        
    - Que `Access-Control-Allow-Origin` **sea exactamente** el mismo dominio que el valor de `Origin` de la petición.
        
    
    En nuestro ejemplo:
    
    - El navegador ve `Origin: https://evil.com` en la petición.
        
    - En la respuesta ve `Access-Control-Allow-Origin: https://evil.com` y `Allow-Credentials: true`.  
        Como coinciden, **le dice al JavaScript de `evil.com`**: “vale, puedes acceder al cuerpo de la respuesta y las cookies incluidas”.
        
4. **¿Por qué “origen concreto” y no `*`?**
    
    - Si el servidor hubiera enviado `Access-Control-Allow-Origin: *` **y** `Allow-Credentials: true`, el navegador **ignora** el `*` y **no** permitiría leer la respuesta con cookies.
        
    - Pero al ver un dominio **específico** (`https://evil.com`), el navegador sí respeta las credenciales.
        
5. **¿Cuál es el peligro?**  
    Porque desde `evil.com` puedes ahora:
    
    - Leer datos sensibles (por ejemplo, el balance bancario).
        
    - Hacer peticiones “en nombre del usuario” (usar `fetch` con `POST`, `DELETE`, etc.) y que se envíen las cookies de sesión, permitiendo incluso modificar datos.