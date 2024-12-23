Con esto elejimos el numero 3 para hacer referencia al archivo file
```bash
exec 4<> file

#de esta manera mandamos cosas a ese descriptor
❯ echo "hola" >&4
❯ cat file
───────┬────
       │ File: file
───────┼────
   1   │ hola

# asi se cierra el descriptor
❯ exec 4>&-
```

Tambien podemos crear una copia del descriptor de archivo 4 con otro descriptor nuevo de tal manera que ademas de lo que le metamso al nuevo descriptor tambien traera lo del descriptor 4
	`exec 8>&4`

> Nota: En /etc/passwd podemos ver los usuarios exitentes y vemos si son logeableas o no

Para ver mas comando de [linux](https://ciberninjas.com/chuleta-comandos-linux/)