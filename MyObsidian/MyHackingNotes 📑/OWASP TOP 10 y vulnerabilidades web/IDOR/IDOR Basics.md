Un **IDOR (Insecure Direct Object Reference)** es una vulnerabilidad de control de acceso en la que un atacante puede acceder, modificar o eliminar datos sin la autorización adecuada, simplemente manipulando identificadores en una solicitud.

- Para testear este tipo de bugs primero hay que crear dos cuentas para poder hacer los tests sobre ellas
- Cuando estes buscando información de entrada recorda buscar los campos ocultos si es que existen `<input type="hidden" name="admin" value="no">`