---
aliases:
  - Chattr
  - Lsattr
---
---
Con el comando lsatrr listamos las flags de una archivo y con el comando chattr podemos cambiar las flags

```bash 
# en este caso el parametro -i es de inmutable por lo que ni el root puede borrarlo aunque simplemente puede sacarle la flag
❯ chattr +i -V test
chattr 1.47.0 (5-Feb-2023)
Las banderas de test están puestas como ----i---------e-------
❯ lsattr
--------------e------- ./a
----i---------e------- ./test

# sacar la flag
❯ chattr -i -V test
```
