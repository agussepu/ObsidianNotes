---
tags:
  - Reconocimiento
  - HackingTools
aliases:
  - enumeracion de puertos alternativa
---
---
La enumeración de puertos es una tarea crucial en las pruebas de penetración y seguridad de redes. Tal y como hemos visto, Nmap es una herramienta de línea de comandos ampliamente utilizada para esta tarea, pero existen alternativas para realizar la enumeración de puertos de manera efectiva sin utilizar herramientas externas.

Una alternativa a la enumeración de puertos utilizando herramientas externas es aprovechar el poder de los **descriptores de archivo** en sistemas **Unix**. Los descriptores de archivo son una forma de acceder y manipular archivos y dispositivos en sistemas Unix. En particular, la utilización de **/dev/tcp** permite la conexión a un host y puerto específicos como si se tratara de un archivo en el sistema.

Para realizar la enumeración de puertos utilizando **/dev/tcp** en Bash, es posible crear un script que realice una conexión a cada puerto de interés y compruebe si el puerto está abierto o cerrado en función de si se puede enviar o recibir datos. Una forma de hacer esto es mediante el uso de comandos como “**echo**” o “**cat**“, aplicando redireccionamientos al **/dev/tcp**. El código de estado devuelto por el comando se puede utilizar para determinar si el puerto está abierto o cerrado.

```bash
#!/bin/bash

function ctrl_c(){
    echo -e "\n\n[!] Saliendo..."
    tput cnorm; exit 1
}

#Ctrl + c

trap ctrl_c SIGINT

declare -a ports=( $(seq 1 65535) )

function checkPort(){
    (exec 3<> /dev/tcp/$1/$2) 2>/dev/null

    if [ $? -eq 0 ];then
        echo "[+] Host $1 - Port $2 (OPEN)"
    fi

    exec 3<&-
    exec 3>&-
}

tput civis

if [ $1 ]; then
    for port in ${ports[@]}; do
        checkPort $1 $port &
    done
else
    echo -e "\n[!] Uso: $0 <ip-adrress>\n"
fi

wait

tput cnorm
```

Aunque esta alternativa puede ser menos precisa y más lenta que el uso de herramientas especializadas como Nmap, es una opción interesante y viable para aquellos que buscan una solución rápida y sencilla para la enumeración de puertos en sistemas Unix. Además, este enfoque puede proporcionar una mejor comprensión de cómo funcionan los descriptores de archivo en los sistemas Unix y cómo se pueden utilizar para realizar tareas de red