Se ve que si el server permite un solo metodo (Depende de como este configurado el server) se puede utilizar un metodo que querramos pero sobreescribiendolo

El server solo permitía peticiones POST

`GET /my-account/change-email?email=aaaaaa%40gmail.com&_method=POST
`

1. **La petición es un GET** (lo indica el navegador o cliente al enviarla).
    
2. **El parámetro `_method=POST`** se usa para "decirle" al servidor que debería tratarla _como si_ fuera una POST.
    
3. El servidor debe tener **lógica explícita para interpretar `_method`** y ejecutar el código correspondiente a un `POST`.
    