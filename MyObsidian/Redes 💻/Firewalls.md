---
tags:
  - Redes
---
Un **firewall** es un sistema de seguridad que controla y filtra el tráfico de red entre dispositivos o redes, siguiendo un conjunto de reglas predefinidas. Su objetivo principal es proteger un sistema o red de accesos no autorizados mientras permite el tráfico legítimo. Existen físicos y virtuales

---

### Tipos de firewalls y su funcionamiento:

#### 1. **Firewall de filtrado de paquetes (Packet Filtering Firewall)**:

- **Cómo funciona**: Inspecciona los encabezados de los paquetes de datos (IP, puerto, protocolo, etc.) y decide si permitir o bloquearlos según reglas configuradas.
- **Características**:
    - Opera en la capa de red (capa 3 del modelo OSI).
    - Es rápido, pero no analiza el contenido de los paquetes.
- **Ejemplo**: Bloquear el acceso al puerto 80 desde una IP específica.
- **Limitación**: No puede distinguir si un paquete es parte de una conexión legítima.

---

#### 2. **Stateful Firewall (Firewall con inspección de estado)**:

- **Cómo funciona**: Monitorea el estado de las conexiones activas y toma decisiones basadas en el contexto de la sesión (si un paquete pertenece a una conexión válida o no).
- **Características**:
    - Opera en las capas de red y transporte (capas 3 y 4).
    - Más seguro que el filtrado de paquetes porque entiende las conexiones activas.
- **Ejemplo**: Permitir solo respuestas a solicitudes salientes legítimas.
- **Limitación**: No analiza el contenido profundo de los paquetes (payload).

---

#### 3. **UTM (Unified Threat Management)**:

- **Cómo funciona**: Es un dispositivo o software que combina múltiples funciones de seguridad en una sola plataforma (firewall, antivirus, control de contenido, prevención de intrusiones, etc.).
- **Características**:
    - Protección integral contra amenazas avanzadas.
    - Opera en múltiples capas del modelo OSI.
    - Facilita la administración centralizada.
- **Ejemplo**: Un UTM puede bloquear sitios maliciosos, detectar malware y filtrar tráfico no deseado al mismo tiempo.
- **Limitación**: Puede ser más lento debido a su complejidad.

---

#### 4. **Servidor proxy firewall (Proxy Firewall)**:

- **Cómo funciona**: Actúa como intermediario entre un cliente y un servidor, filtrando el tráfico mediante inspección a nivel de aplicación.
- **Características**:
    - Opera en la capa de aplicación (capa 7 del modelo OSI).
    - Puede analizar el contenido completo de los paquetes (Deep Packet Inspection).
    - Ofrece anonimato, ya que las conexiones externas ven solo la IP del proxy.
- **Ejemplo**: Bloquear solicitudes HTTP hacia dominios específicos.
- **Limitación**: Puede ser más lento y menos escalable en redes grandes.

---

#### 5. **Firewall de última generación (Next-Generation Firewall o NGFW)**:

- **Cómo funciona**: Combina las funciones de firewalls tradicionales (filtrado de paquetes y stateful inspection) con características avanzadas como inspección profunda de paquetes (DPI), detección de intrusiones (IDS/IPS), y análisis de aplicaciones.
- **Características**:
    - Opera desde la capa de red hasta la de aplicación.
    - Puede identificar y controlar aplicaciones específicas (como bloquear el uso de Facebook pero permitir WhatsApp).
    - Protección avanzada contra amenazas modernas (como ataques de día cero).
- **Ejemplo**: Detectar y bloquear tráfico malicioso encriptado en HTTPS.
- **Limitación**: Costos más elevados y requiere mayor capacidad de procesamiento.

---

### Comparación rápida:

|**Tipo**|**Capa OSI**|**Capacidades**|**Uso común**|
|---|---|---|---|
|Filtrado de paquetes|Red (capa 3)|Básico, rápido, reglas simples|Pequeñas redes o sistemas básicos|
|Stateful Firewall|Red y Transporte|Conexiones válidas, más seguro|Redes corporativas|
|UTM|Varias capas|Protección integral|PYMEs, empresas|
|Proxy Firewall|Aplicación (capa 7)|Inspección profunda, anonimato|Control granular de tráfico|
|NGFW|Todas las capas|Avanzado, DPI, IDS/IPS|Empresas grandes, alta seguridad|
