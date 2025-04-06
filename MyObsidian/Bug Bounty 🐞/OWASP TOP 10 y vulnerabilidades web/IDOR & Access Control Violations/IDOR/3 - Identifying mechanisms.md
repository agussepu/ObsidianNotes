---
tags:
  - BugBounty
---
---
***Recordatorio***: La verificación de un usuario no necesariamente se da con un user id puede darse simplemente con el user o cualquier dato 

Debemos identificar cada **mecanismo** de la web que sea un oportunidad para nosotros debemos ir anotando en caso de poder cargar datos, anotar si es una solicitud GET o en caso que sea un actualización de datos si es una solicitud POST y asi con cada mecanismo.

- En este ejemplo a la hora de actualizar los datos se usa una solicitud POST la cual también utiliza un user id en alguna parte para identificar al usuario (hay que tener en cuenta que no hay certeza de que lo identifique del mismo modo qque la solicitud GET que vimos antes)
