---
tags:
  - Redes
aliases: []
---
---
#  TCP (Transmisión Control Protocol)

## Características principales:
1. **Conexión orientada**: TCP establece una conexión entre el cliente y el servidor antes de transmitir datos (conocido como el **handshake de tres pasos**):
    
    - El cliente envía un paquete SYN (solicitud de sincronización).
    - El servidor responde con un paquete SYN-ACK (confirmación de sincronización).
    - El cliente responde con un paquete ACK (confirmación final).
2. **Fiabilidad**:
    - Garantiza que los datos lleguen al destino correctamente y en orden.
    - Si un paquete se pierde o llega corrupto, TCP lo retransmite.
3. **Control de flujo**:
    - Ajusta la velocidad de envío de datos según la capacidad del receptor, evitando sobrecargas.
4. **Segmentación y reensamblaje**:
    - Divide los datos en segmentos y los reensambla en el destino en el orden correcto.
5. **Puertos TCP comunes**:
- 21: **FTP** (File Transfer Protocol) – permite la transferencia de archivos entre sistemas.
- 22: **SSH** (Secure Shell) – un protocolo de red seguro que permite a los usuarios conectarse y administrar sistemas de forma remota.
- 23: **Telnet** – un protocolo utilizado para la conexión remota a dispositivos de red.
- 80: **HTTP** (Hypertext Transfer Protocol) – el protocolo que se utiliza para la transferencia de datos en la World Wide Web.
- 443: **HTTPS** (Hypertext Transfer Protocol Secure) – la versión segura de HTTP, que utiliza encriptación SSL/TLS para proteger las comunicaciones web.
#### **Ventaja**:
- Fiabilidad total en la transmisión de datos.
#### **Desventaja**:
- Mayor latencia y uso de recursos debido a los mecanismos de control y retransmisión.

---
# UDP (User Datagram Protocol)
#### Características principales:
1. **No orientado a conexión**:
    - No establece una conexión antes de enviar datos.
    - Los paquetes se envían directamente al destino sin Handshake.
2. **No fiable**:
    - No garantiza que los datos lleguen ni que lo hagan en orden.
    - No hay retransmisión en caso de pérdida.
3. **Velocidad**:
    - Es más rápido que TCP, ya que no hay mecanismos de control de flujo o reensamblaje
    - 
4. **Puertos UDP comunes**:
- 53: **DNS** (Domain Name System) – un sistema que traduce nombres de dominio en direcciones IP.
- 67/68: **DHCP** (Dynamic Host Configuration Protocol) – un protocolo utilizado para asignar direcciones IP y otros parámetros de configuración a los dispositivos en una red.
- 69: **TFTP** (Trivial File Transfer Protocol) – un protocolo simple utilizado para transferir archivos entre dispositivos en una red.
- 123: **NTP** (Network Time Protocol) – un protocolo utilizado para sincronizar los relojes de los dispositivos en una red.
- 161: **SNMP** (Simple Network Management Protocol) – un protocolo utilizado para administrar y supervisar dispositivos en una red.
#### **Ventaja**:
- Baja latencia y menor uso de recursos.
#### **Desventaja**:
- No asegura la entrega de datos ni su integridad.

---

# Comparación básica

| **Característica** | **TCP**              | **UDP**                  |
| ------------------ | -------------------- | ------------------------ |
| Orientación        | Conexión (Handshake) | Sin conexión             |
| Fiabilidad         | Garantizada          | No garantizada           |
| Velocidad          | Más lento            | Más rápido               |
| Orden de los datos | Garantizado          | No garantizado           |
| Uso típico         | Servicios críticos   | Servicios en tiempo real |
