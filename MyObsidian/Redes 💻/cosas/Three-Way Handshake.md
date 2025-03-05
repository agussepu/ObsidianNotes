---
tags:
  - Redes
aliases:
  - Three-Way Handshake
---
---
El **Three-Way Handshake** es el proceso que TCP usa para establecer una conexión entre un cliente (por ejemplo, tu computadora) y un servidor (por ejemplo, un servidor web). Este proceso consta de tres pasos básicos que aseguran que ambas partes estén listas para comunicarse. Aquí te lo explico con más detalle:

![[handshake.png]]

---
### Pasos del Three-Way Handshake

1. **SYN (Synchronize)**:
    - El cliente quiere iniciar una conexión y envía un paquete TCP con el flag **SYN** activado al servidor.
    - Este paquete incluye:
        - Un número de secuencia inicial (**Sequence Number**, o simplemente **Seq**), que es un número aleatorio usado para identificar el inicio de los datos que el cliente enviará.
    - **Objetivo**: El cliente dice al servidor: "¡Quiero conectar contigo y este es mi número de secuencia inicial!"
    
    **Ejemplo real:**
    - Cliente envía: `SYN=1, Seq=1000`.

---

2. **SYN-ACK (Synchronize + Acknowledge)**:    
    - El servidor recibe el paquete SYN y responde con un paquete **SYN-ACK**.
    - Este paquete incluye:
        - El flag **SYN** (para sincronizar el servidor con el cliente).
        - El flag **ACK** (para confirmar que recibió el SYN del cliente).
        - Un número de secuencia inicial propio del servidor (**Seq**).
        - Un número de confirmación (**Acknowledgment Number**, o **Ack**), que es el número de secuencia del cliente incrementado en 1.
    - **Objetivo**: El servidor dice al cliente: "¡Recibí tu solicitud! Aquí está mi número de secuencia inicial y confirmo haber recibido tu número."
    
    **Ejemplo real:**
    
    - Servidor envía: `SYN=1, ACK=1, Seq=3000, Ack=1001`.

---

3. **ACK (Acknowledge)**:
    
    - El cliente recibe el paquete **SYN-ACK** del servidor y responde con un paquete **ACK**.
    - Este paquete incluye:
        - El flag **ACK** activado, para confirmar que recibió el SYN del servidor.
        - Un número de confirmación (**Ack**), que es el número de secuencia del servidor incrementado en 1.
    - **Objetivo**: El cliente dice al servidor: "¡Confirmo que recibí tu SYN y tu número de secuencia inicial!"
    
    **Ejemplo real:**
    
    - Cliente envía: `ACK=1, Seq=1001, Ack=3001`.

---

### **Resumen del intercambio**

1. Cliente → Servidor: `SYN=1, Seq=1000`
2. Servidor → Cliente: `SYN=1, ACK=1, Seq=3000, Ack=1001`
3. Cliente → Servidor: `ACK=1, Seq=1001, Ack=3001`

---

### **Propósito del Three-Way Handshake**
- **Sincronización**: Ambos lados acuerdan números de secuencia iniciales para rastrear los datos.
- **Conexión establecida**: Confirma que el cliente y el servidor están listos para intercambiar datos.
- **Detección de errores**: Si algún paso falla, la conexión no se establece.

---

### Visualización simple
Imagina que es como un saludo formal:
1. **Cliente**: "Hola, ¿puedo hablar contigo?" (SYN)
2. **Servidor**: "Claro, hablemos. Hola, ¿me escuchas?" (SYN-ACK)
3. **Cliente**: "Sí, te escucho. ¡Hablemos!" (ACK)

### Comunicación después del Three-Way Handshake
1. Una vez que el **Three-Way Handshake** se completa, la comunicación entre cliente y servidor fluye normalmente:
    - Los datos van y vienen en segmentos TCP.
    - Cada segmento incluye un **número de secuencia (Seq)** y un **número de confirmación (Ack)** para garantizar que los datos se envíen y reciban correctamente.
2. Cada vez que el cliente o servidor recibe datos, envía un **ACK** (Acknowledgment) para confirmar la recepción.
---
# Cierre de la conexión TCP (Four-Way Handshake)

Al finalizar la comunicación, TCP utiliza un proceso de **Four-Way Handshake** para cerrar la conexión de manera ordenada. Este proceso consta de cuatro pasos, y aquí es donde aparece el **ACK final**.

1. **FIN (Finish)**:
    
    - Una de las partes (por ejemplo, el cliente) decide cerrar la conexión y envía un paquete **FIN** al servidor.
    - Esto indica: "Ya no tengo datos que enviarte".
2. **ACK (Acknowledgment)**:
    
    - La otra parte (el servidor) responde con un paquete **ACK** para confirmar que recibió el **FIN**.
    - Esto indica: "Entendido, sé que ya no me enviarás más datos".
3. **FIN (Finish)**:
    
    - Si el servidor también ha terminado de enviar datos, enviará su propio paquete **FIN** al cliente.
    - Esto indica: "Yo también he terminado, y quiero cerrar la conexión".
4. **ACK (Acknowledgment)**:
    
    - Finalmente, el cliente responde con un **ACK** para confirmar que recibió el **FIN** del servidor.
    - Esto cierra completamente la conexión.

---

### **Resumen del cierre de conexión (Four-Way Handshake)**
1. Cliente → Servidor: `FIN=1, Seq=1001`  
    ("No tengo más datos que enviar.")
2. Servidor → Cliente: `ACK=1, Seq=3001, Ack=1002`  
    ("Entendido, sé que terminaste.")
3. Servidor → Cliente: `FIN=1, Seq=3001`  
    ("Yo también terminé.")
4. Cliente → Servidor: `ACK=1, Seq=1002, Ack=3002`  
    ("Entendido, la conexión está cerrada.")

---

# ¿Por qué se usa este proceso?
El cierre ordenado asegura que:
1. Ambas partes sepan que ya no hay más datos que enviar.
2. Los recursos (como puertos) se liberen correctamente en ambos lados.
3. Se minimicen errores o pérdidas de datos.
---
### Diferencias entre el inicio y el cierre

- **Inicio** (**Three-Way Handshake**): SYN → SYN-ACK → ACK.
- **Cierre** (**Four-Way Handshake**): FIN → ACK → FIN → ACK.

---
### ¿Qué pasa si no se hace el cierre correctamente?
- Si una parte no envía un **FIN**, la conexión puede quedar en un estado llamado **TIME_WAIT**, ocupando recursos innecesariamente.
- Esto es común en ataques de tipo **DoS (Denial of Service)**, donde se envían múltiples SYN sin completar la conexión (SYN Flood).