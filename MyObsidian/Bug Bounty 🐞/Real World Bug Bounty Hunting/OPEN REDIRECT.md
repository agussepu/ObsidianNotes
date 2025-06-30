## Resumen: Cómo Funcionan los Open Redirects

Un **Open Redirect** ocurre cuando una aplicación web permite redirigir al usuario a una URL externa sin validar adecuadamente el destino. Esta redirección puede estar basada en:

- Parámetros en la URL (por ejemplo: `redirect=`, `next=`, `url=`, etc.)
- Etiquetas HTML `<meta>` con `http-equiv="refresh"`
- Redirecciones usando JavaScript (como `window.location`)
### Ejemplo típico
```plaintext
https://www.ejemplo.com/?redirect_to=https://www.sitiolegitimo.com
```

Si la aplicación no valida el parámetro `redirect_to`, un atacante puede reemplazarlo con una URL maliciosa:

`https://www.ejemplo.com/?redirect_to=https://www.sitio-malicioso.com`

Cuando la víctima accede al enlace, el navegador realiza una solicitud GET al sitio legítimo, que luego responde con un código de redirección (como 302) e indica al navegador que se dirija a la URL del atacante mediante el encabezado `Location`.