**IDOR (Insecure Direct Object Reference)** es un tipo de vulnerabilidad donde una aplicación **permite acceder o modificar objetos directamente** (como usuarios, archivos, pedidos, mensajes) **sin validar si el usuario tiene permiso** para hacerlo.

- ***IDOR***: cuando un usuario visita una pagina de perfil, una API manda el valor del user id al servidor back-end. El server responde con un gran conjunto de datos incluyendo data sensible basada en el valor del user id enviado. Si una atacante puede enviar otro user id y recibir datos a los cuales no deberia de tener acceso, entonces estariamos hablando de un IDOR

- ***Access Control Violations***: Un usuario con rol de administrador puede acceder a la pagina que permite ver datos sensibles de otros usuarios. Dicho mecanismo solo es valido para usuarios que tengan dicho rol. Si un usuario o atancante con otro rol tiene acceso a este mecanismo estamos hablando de un Access control violation
