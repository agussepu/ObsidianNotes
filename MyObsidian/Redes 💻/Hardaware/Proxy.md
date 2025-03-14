---
tags:
  - Redes
---
Un **proxy** es un servidor intermediario que actúa como un puente entre un cliente (por ejemplo, tu computadora) y un servidor (por ejemplo, un sitio web o servicio en línea). Cuando usas un proxy, tus solicitudes de red no van directamente al servidor final, sino que pasan primero por el proxy, que las reenvía al destino. De manera similar, las respuestas del servidor pasan primero por el proxy antes de llegar a ti.

---

### Funcionalidades de un Proxy

1. **Ocultación de la IP del cliente**:
    
    - El servidor final ve la IP del proxy en lugar de la IP del cliente. Esto proporciona cierto nivel de anonimato.
2. **Filtrado de contenido**:
    
    - Puede bloquear o permitir el acceso a ciertos sitios web o servicios según las políticas configuradas (por ejemplo, bloquear redes sociales en una oficina).
3. **Control de acceso**:
    
    - Permite administrar quién puede acceder a ciertos recursos en la red, basándose en credenciales o direcciones IP.
4. **Caché de datos**:
    
    - Almacena en caché contenido solicitado con frecuencia (como páginas web), acelerando el acceso a esos recursos para futuros usuarios.
5. **Compresión de datos**:
    
    - Puede comprimir contenido, reduciendo el uso de ancho de banda.
6. **Monitoreo y registro**:
    
    - Registra el tráfico que pasa por él, lo que ayuda en auditorías y monitoreo de uso de la red.
7. **Traducción de protocolos**:
    
    - Puede actuar como un traductor entre diferentes protocolos de red, como convertir HTTP a HTTPS.
8. **Seguridad adicional**:
    
    - Puede actuar como una barrera inicial para proteger a los clientes de ciertos ataques o malware provenientes de internet.

---

### Usos más comunes de un Proxy

1. **Privacidad y anonimato**:
    
    - Navegar de forma anónima al ocultar tu dirección IP real.
2. **Acceso a contenido restringido geográficamente**:
    
    - Usar un proxy ubicado en otro país para acceder a servicios o sitios bloqueados en tu región.
3. **Control en redes corporativas**:
    
    - Limitar el acceso de los empleados a ciertos sitios durante el horario laboral.
4. **Reducción de ancho de banda**:
    
    - Optimizar el uso del ancho de banda mediante la caché de recursos.
5. **Acceso a internet en redes locales**:
    
    - En algunos entornos, los usuarios deben conectarse a través de un proxy para acceder a internet.
6. **Pruebas y depuración**:
    
    - Desarrolladores y administradores de red usan proxies para analizar el tráfico entre clientes y servidores.
7. **Seguridad en entornos escolares o públicos**:
    
    - Implementar controles para evitar que estudiantes o usuarios de redes públicas accedan a contenido inapropiado.

---

### Tipos de Proxies

1. **Proxy HTTP**:
    
    - Maneja solicitudes y respuestas HTTP. Ideal para navegación web.
2. **Proxy HTTPS (SSL Proxy)**:
    
    - Similar al HTTP, pero soporta conexiones cifradas.
3. **Proxy SOCKS**:
    
    - Opera a nivel más bajo que HTTP/HTTPS y soporta tráfico de cualquier protocolo, como FTP, torrents, o juegos.
4. **Proxy inverso (Reverse Proxy)**:
    
    - En lugar de proteger al cliente, protege los servidores finales y distribuye el tráfico entrante.
5. **Proxy transparente**:
    
    - Intercepta el tráfico sin necesidad de que el cliente lo configure explícitamente.