---
tags:
  - WriteUp
---
---
*Maybe:*
Based on my understanding, I’ve selected CWE-639 and estimated the severity as Medium. I’m open to corrections if the impact is different based on your internal models

This is my first HackerOne report and I’ve followed the Zooplus program guidelines. I’m happy to receive any feedback o | Bug Bounty PoCr suggested improvements. Thanks for your time

----

# Título

Account Takeover vía manipulación de cookies y reutilización de JWT 

---

# Descripcion
## Resumen
Es posible obtener el `JWT` de otro usuario autenticado (usuario B) simplemente reemplazando las cookies `mzpStickySession` y `MZPSID` en una sesión activa de otro usuario (usuario A) obteniendo información como nombre, customerId, email y mas información privilegiada. El servidor devuelve un token JWT válido del usuario B, que luego puede usarse para realizar acciones autenticadas, como modificar el nombre y apellido  del usuario B, desde la sesión de A utilizando el `JWT` obtenido y las cookies `mzpStickySession` y `MZPSID`.

---
## Pasos para reproducir

1. Iniciar sesión con el usuario A (Izquierda) y el usuario B (Derecha).
![[sesiones.png]]
    
2. Obtener cookies `mzpStickySession` y `MZPSID` de usuario B (por ejemplo, desde otra cuenta controlada).
![[cookies.png]]
    
3. Reemplazar el valor de las cookies `mzpStickySession` y `MZPSID` del usuario B en las del usuario A y enviar la request (en este caso me encuentro usando Caido).
![[CookieNoEdit.png]]

![[CookiesEdit.png]]


4. En el response recibimos el `JWT` del usuario B.
![[JWT.png]]

5. Con esto podemos usar ese `JWT` y las cookies `mzpStickySession` y `MZPSID`  para por ejemplo modificar el nombre y apellido del usuario B desde la sesión de A en una request `PUT` a `/customer-data/api/v2/basicData`.

	Request usada para el cambiar el nombre del usuario desde el usuario A con cookies  `mzpStickySession`, `MZPSID`  y `JWT` del usuario B :
	
```http
PUT /customer-data/api/v2/basicData HTTP/1.1
Host: www.zooplus.com
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:138.0) Gecko/20100101 Firefox/138.0
Accept: application/json, text/plain, */*
Accept-Language: es-AR,es;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate, br, zstd
Content-Type: application/json
X-Domain: zooplus.com
X-Site-Id: 2
Authorization: Authorization: Bearer <JWT_OBTENIDO_DEL_USUARIO_B>
Content-Length: 43
Origin: https://www.zooplus.com
Connection: keep-alive
Referer: https://www.zooplus.com/account/customer/editPersonalInformation
Cookie: mzpStickySession="b525f0a78e9777fc"; MZPSID=F5A811D36DD4F8EFEF91BC7A894D6FA1; 
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
Priority: u=0

{"firstName":"Hack","lastName":"Hacked"}
```
    
6. Verificar que el nombre y apellido de la cuenta B cambian, confirmando control efectivo.
    ![[change.png]]

---

## Impacto

- Permite la **toma parcial de cuenta** (Account Takeover) sin necesidad de contraseña ni interacción de la víctima.
    
- Filtración de **JWT de otros usuarios** mediante manipulación simple de cookies.
    
- Uso del token filtrado para **modificar datos personales** de la cuenta víctima.
    
- Riesgo de robo de identidad, fraude, suplantación y pérdida de reputación.

Este comportamiento demuestra una falla crítica en el aislamiento de sesión y control de autenticación. Es explotable de forma automatizada y afecta directamente a los usuarios autenticados.

![[Pasted image 20250518174405.png]]


![[CookieMod.png]]