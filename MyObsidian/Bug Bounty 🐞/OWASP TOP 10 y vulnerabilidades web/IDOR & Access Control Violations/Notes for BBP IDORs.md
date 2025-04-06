---
tags:
---
---
## Pointers 
Aca vamos a ir anotado cualquier cosa que pueda ser indicio de otra vulnerabilidad o algo que me de indicio de que el equipo de seguridad no usa buenas practicas por lo que podria explotarse en un futuro.

## Accounts
Esta sección se debe ya que a la hora de buscar un IDOR necesitamos mas de una cuenta. La siguiente practicas son empleadas para que los devs puedan identificar que son cuentas de test y puedan eliminarlas en un futuro si es necesario 
- Registraremos las cuentas con `@wearehackerone.com`
- Usaremos la notación `+` para registrar varias cuentas (cualquier cosa luego del mas se ignora por lo que los mails llegarian a la cuenta que pongas antes del mas)
Example: `agussepu+demo1@wearehackerone.com` 

## Mechanisms
Aca vamos a ir anotando cada mecanismo  ( Cargar datos del usuario, Cambiar datos del usuario, etc)

## Objects


----
# Ejemplo
![[exampleNoteBBP1.png]]
![[exampleNoteBBP.png]]
![[NoteBBP_IDOR.png]]