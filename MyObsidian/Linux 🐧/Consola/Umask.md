Se usa para establecer los permisos que tendran los ficheros o directorios que se creen en dicha carpeta. directorios 777 ficheros 666 y se les resta la umask  

### **📌 `umask` vs `chmod`: Diferencias y Usos**

Tanto `umask` como `chmod` controlan los **permisos de archivos en Linux**, pero tienen propósitos distintos:

| **Comando** | **Función**                                                                   |
| ----------- | ----------------------------------------------------------------------------- |
| `umask`     | Define los **permisos predeterminados** de los nuevos archivos y directorios. |
| `chmod`     | Modifica manualmente los permisos de un archivo o directorio ya existente.    |

---

### **🔹 `umask`: Establece permisos por defecto**

Cuando creas un archivo o directorio, el sistema usa un valor base de permisos y luego aplica la **máscara de permisos (`umask`)** para restringir ciertos permisos.

#### **Ejemplo de `umask`**

```bash
umask 022
```

Esto significa que los nuevos archivos y directorios tendrán permisos predeterminados **más restrictivos**.

**Cálculo de permisos:**

1. **Permisos base**:
    - Archivos → `666` (lectura y escritura para todos).
    - Directorios → `777` (lectura, escritura y ejecución para todos).
2. **Aplicando `umask`** (restando los bits correspondientes):
    - `666 - 022 = 644` (archivos: `rw-r--r--`).
    - `777 - 022 = 755` (directorios: `rwxr-xr-x`).

📌 **Para ver tu `umask` actual:**

```bash
umask
```

📌 **Para cambiar el `umask` en la sesión actual:**

```bash
umask 027
```

Esto haría que los nuevos archivos sean `640` (`rw-r-----`) y los directorios `750` (`rwxr-x---`).

---

### **🔹 `chmod`: Cambia permisos de archivos existentes**

Mientras `umask` afecta **nuevos archivos**, `chmod` te permite cambiar permisos de archivos ya creados.

#### **Ejemplo de `chmod`**

```bash
chmod 644 archivo.txt
```

Esto cambia manualmente los permisos de `archivo.txt` a `rw-r--r--`.

#### **Comparación rápida**

| Acción                               | `umask` | `chmod` |
| ------------------------------------ | ------- | ------- |
| Afecta **nuevos archivos**           | ✅       | ❌       |
| Afecta **archivos existentes**       | ❌       | ✅       |
| Define permisos predeterminados      | ✅       | ❌       |
| Permite cambiar permisos manualmente | ❌       | ✅       |

---

### **📌 ¿Cuándo usar `umask` y cuándo `chmod`?**

- Usa **`umask`** si quieres establecer permisos predeterminados **para todos los archivos que crees**.
- Usa **`chmod`** si necesitas cambiar los permisos de **un archivo o directorio específico** después de crearlo.

Si tienes alguna duda más, dime qué caso necesitas resolver. 🚀