---
tags:
  - BugBounty
---
---
# Estado
Quedo ese vector de ataque donde mediante dos cookies puedo robar el JWT, pero por ahora no encontrar una forma de obtener dichas cookies sin tener acceso a la otra cuenta, parece que las mejores opciones son encontrar un XSS o un CSRF pero no se bien como funcionan aunque intente CSRF pero el CORS parece bloquear mis peticiones (intente esto ya que las cookie carecen de SameSite)




---
## Scope
**Domain**: https://www.zooplus.com/account/overview

---
## Accounts
- *Account 1*: agussepu+demo1@wearehackerone.com 
	- Contraseña: Ayg20189
	- Nombre: Agustin
	- Apellido: Sepu
	- **Customer Number** 50539776

- *Account 2*: agussepu+demo2@wearehackerone.com 
	- Contraseña: Ayg20189
	- Nombre: Max
	- Apellido: Rodriguez
	- **Customer Number** 



---
## Pointers

#### Cookies necesarias
Solo se necesitan dos cookies para identificar al usuario `mzpStickySession y MZPSID`

```http
Cookie: mzpStickySession="35e35b6f6307a558"; MZPSID=607CB4DCD9739C4DE9923EA6A043203E; 
```

---
## Tracking

**Reporte N°1:**

**Test 1:** Parece ser que al cambiar las dos cookies se produce un IDOR, pero ambas sesiones deben estar abiertas ya que interpreto que deben caducar dichas cookies al cerrar la session y ademas deben cambiarse ambas cookies, si se cambia una sola la validación no se da.

**Test 2:** Cerre el navegador con la cuenta 2 y mande la petición con esas cookies y sigue funcionando. Parece que no importa que este abierta o no la sesión, o tal vez dure un rato. 

**Test 3:** Pobre desde la session A poner cookies viejas de la session B y parece que no funciona, tengo que volver a probar.

**Test 4**: Parece que la vulnerabilidad no era tal ya que al cambiar las cookies obtengo por un momento la info del usuario B pero no el control de su cuenta solo obtengo su mail, nombre y appellido parece mas un information leak que otra cosa, seguire probando por un IDOR antes de mandar reporte por leak

**Test 5**: La euforia bajo voy a ver si puedo avanzar el IDOR y ver donde se vuelve a validar el usuario

**Test 6:** Parece que existe el IDOR pero solo desde firefox, ahora intentare automatizar el cambio de cookies con burpsuite pq no me funciona en caido el de MZPSID.

**Test 7**: Por alguna razon en un punto empieza a usar el JWT del usuario en uso y no de la victima automatizare el cambio de jwt y vere que pasa para ir terminando.

---
**Reporte N°2:** Me marcaron el reporte como informativo ya que debo demostrar como obtener dichas cookies.

**Test 1**: Intentara un CSRF para obtener las cookies de un usuario.

**Test 2**: Estaba haciendo vibe hacking puro estaba en cualquiera ya ahora se que debo de buscar obtener las cookies de alguna manera, probablemente sea un XSS aunque nose todavía como concha se hacen. Ademas nose cuanto tiempo tengo ya la empresa tiene la información de la vuln

**Test 3**: 
