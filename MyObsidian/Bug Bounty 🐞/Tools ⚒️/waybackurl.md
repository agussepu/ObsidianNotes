## **🔍 Waybackurls en Bug Bounty: ¿Para qué sirve y cómo usarlo?**

📌 **Waybackurls** es una herramienta que se usa en bug bounty para **recuperar URLs antiguas** de un dominio. Se basa en **Wayback Machine (archive.org)**, que guarda copias de sitios web con el tiempo.

💡 **¿Por qué es útil en bug bounty?**  
1️⃣ **Descubre endpoints eliminados o deshabilitados**, que podrían seguir siendo accesibles.  
2️⃣ **Encuentra parámetros vulnerables en versiones antiguas** de la web.  
3️⃣ **Recupera archivos JS antiguos**, que pueden exponer endpoints API internos.  
4️⃣ **Identifica páginas con funciones sensibles** (ejemplo: `/admin`, `/debug`, `/backup`).

---

## **🚀 Cómo usar waybackurls en Bug Bounty**

### **🟢 1️⃣ Instalación en Linux**

```bash
go install github.com/tomnomnom/waybackurls@latest
```

Si ya tienes Go instalado, lo ejecutas con:

```bash
export PATH=$HOME/go/bin:$PATH
```

Ahora puedes correr `waybackurls` desde cualquier lugar.

---

### **🟡 2️⃣ Usar waybackurls para encontrar endpoints ocultos**

```bash
echo "target.com" | waybackurls
```

Esto devuelve **todas las URLs antiguas indexadas en Wayback Machine**.

📌 **Ejemplo de salida:**

```
https://target.com/admin/login
https://target.com/api/v1/users
https://target.com/old/backup.zip
https://target.com/test.php?id=1
https://target.com/js/config.js
```

🔹 **¿Cómo aprovechar esto?**

- `/admin/login` ➝ Podría seguir accesible (prueba fuzzing).
    
- `/old/backup.zip` ➝ **¡Revisar si aún existe!** Puede contener credenciales.
    
- `/test.php?id=1` ➝ **Probar SQLi en `id=1`**.
    
- `/js/config.js` ➝ Puede revelar claves API o endpoints internos.
    

---

### **🟠 3️⃣ Filtrar URLs útiles**

Si quieres buscar solo URLs con parámetros (`?`), usa:

```bash
echo "target.com" | waybackurls | grep "?"
```

🔹 **Ejemplo de salida:**

```
https://target.com/search.php?q=admin
https://target.com/view.php?id=123
https://target.com/download.php?file=config
```

📌 **Pruebas a hacer:**  
✅ **SQL Injection** en `id=123`.  
✅ **LFI (Local File Inclusion)** en `file=config`.  
✅ **XSS en `q=admin`**.

---

### **🔴 4️⃣ Combinar waybackurls con otras herramientas**

**📌 Buscar subdominios + URLs antiguas**

```bash
subfinder -d target.com | waybackurls
```

🔹 Esto te da URLs antiguas **de todos los subdominios del objetivo**.

**📌 Buscar solo archivos JS (pueden contener claves API)**

```bash
echo "target.com" | waybackurls | grep ".js"
```

Ejemplo de salida:

```
https://target.com/static/app.js
https://target.com/api/config.js
```

📌 **Si `config.js` sigue disponible, revisa si contiene claves API.**

---

## **🎯 Conclusión**

✅ **Waybackurls te ayuda a encontrar endpoints ocultos y URLs antiguas**.  
✅ **Ideal para descubrir archivos JS con información sensible**.  
✅ **Se puede combinar con herramientas como subfinder y gau** para ampliar resultados.  
✅ **Muy útil para encontrar SQLi, XSS, LFI en parámetros antiguos**.

🔥 **Si necesitas ejemplos más avanzados, dime y lo ajustamos a tu objetivo en bug bounty.** 🚀