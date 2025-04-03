---
tags:
  - HackingTools
---
---
# **🔹 1️⃣ Configuración de SQLMap para Minimizar Ruido**

Para evitar llamar la atención, usa opciones para reducir la agresividad de SQLMap.

📌 **Comandos esenciales:**

```bash
sqlmap -u "https://target.com/profile.php?id=1" --dbs --random-agent --delay=2 --batch --level=3 --risk=2
```

🔹 **Explicación de opciones:**  
✅ `--random-agent` → Usa un **User-Agent aleatorio** para evitar detección.  
✅ `--delay=2` → Espera **2 segundos entre cada petición** (reduce detección y previene baneos).  
✅ `--batch` → Evita preguntas interactivas de SQLMap.  
✅ `--level=3` → Aumenta la detección de SQLi sin ser extremadamente agresivo.  
✅ `--risk=2` → Prueba payloads más seguros para evitar DoS accidental.

---

# **🔸 2️⃣ Uso Responsable de SQLMap en Bug Bounty**

📌 **Pasos a seguir antes de correr SQLMap:**  
✅ **1. Revisa el programa en HackerOne:**  
➡️ Si en las reglas dicen **"No Automated Scanning"**, **NO USES SQLMAP**.  
➡️ Si permiten escaneos, sigue las configuraciones de bajo ruido.

✅ **2. Identifica manualmente una posible SQLi:**  
Antes de usar SQLMap, intenta probar manualmente:

```
https://target.com/profile.php?id=1'
https://target.com/profile.php?id=1' OR 1=1 --
```

Si ves errores SQL o cambios en la respuesta, es un **buen indicio** de SQLi.

✅ **3. Usa SQLMap solo en parámetros específicos:**  
Si confirmaste que un parámetro puede ser vulnerable, corre SQLMap en **solo ese parámetro**, en vez de escanear toda la web.

```bash
sqlmap -u "https://target.com/profile.php?id=1" --dbs --risk=1 --level=2 --delay=5
```

✅ **4. Usa `--technique` para limitar tipos de ataque:**  
Si quieres **reducir ruido**, evita técnicas como `B` (Boolean-based Blind) o `T` (Time-based).

```bash
sqlmap -u "https://target.com/profile.php?id=1" --dbs --technique=U --risk=1 --level=2
```

🔹 **Explicación:**

- `--technique=U` → Solo prueba **UNION-based SQLi**.
    
- `--technique=B` → Solo prueba **Boolean-based**.
    
- `--technique=T` → Solo prueba **Time-based** (⚠ Evitar en programas con detección de DoS).
    

✅ **5. Usa `--tamper` para evadir WAFs**  
Si el sitio usa un **firewall**, puedes intentar bypass con scripts de tamper:

```bash
sqlmap -u "https://target.com/profile.php?id=1" --dbs --tamper=space2comment.py --random-agent
```

📌 **Lista de tamper scripts en SQLMap:**

```bash
sqlmap --list-tampers
```

---

# **🔹 3️⃣ Alternativa: Usar Burp Suite en Lugar de SQLMap**

📌 **Si SQLMap genera mucho tráfico, puedes usar Burp Suite para hacer pruebas más controladas.**

1️⃣ **Captura la petición vulnerable con Burp Suite.**  
2️⃣ **Modifica el parámetro y prueba manualmente `' OR 1=1 --`**.  
3️⃣ **Si ves cambios en la respuesta, prueba UNION o Boolean-based manualmente.**  
4️⃣ **Si confirmas SQLi, usa SQLMap solo con opciones de bajo ruido.**

---

# **🚀 Conclusión**

✅ **Sí, puedes usar SQLMap en Bug Bounty**, pero **solo si lo configuras correctamente y el programa lo permite**.  
✅ Usa opciones como **`--delay=2`**, **`--level=3`**, **`--risk=2`** y **`--technique=U`** para hacer pruebas discretas.  
✅ **Evita escaneos masivos** y **prueba manualmente antes de usar SQLMap**.  
✅ **Si el programa prohíbe escaneos automáticos, usa Burp Suite en su lugar.**

🔥 **Si necesitas ayuda con un caso específico, dime y ajustamos la estrategia.** 🚀