https://github.com/soydalto/Curso_De_Python

Filosofía de Python - Zen de Python (legibilidad y simplicidad en el código)

Es un lenguaje de **alto nivel, interpretado y de propósito general**.

**interpretado:** Se ejecutan mediante un interprete sin ser compilado previamente (traduce el código fuente en código maquina en tiempo real a la vez que se ejecuta el programa)

**Alto nivel:** Mas fácil de leer y escribir para los humanos

**Propósito general:**
- ***Programación orientada a objetos (POO)***: 
- ***Programación Imperativa:*** 
- ***Programación Funcional***: 

---
El **intérprete de Python** es el corazón del lenguaje de programación Python; es el motor que ejecuta el código que escriben los programadores. Cuando hablamos del “**intérprete de Python**“, nos referimos al programa que lee y ejecuta el código Python en tiempo real.

**Funciones Clave del Intérprete de Python:**

- **Ejecución de Código**: El intérprete ejecuta el código escrito en Python línea por línea, lo que facilita la depuración y permite a los desarrolladores probar fragmentos de código de forma interactiva.
- **Modo Interactivo**: El intérprete puede usarse en un modo interactivo que permite a los usuarios ejecutar comandos de Python uno a uno y ver los resultados de inmediato, lo cual es excelente para el aprendizaje y la experimentación.
- **Modo de Script**: Además del modo interactivo, el intérprete puede ejecutar programas completos o scripts que se escriben en archivos con la extensión ‘**.py**‘.
- **Compilación a Bytecode**: Aunque Python es un lenguaje interpretado, internamente, el intérprete compila el código a bytecode antes de ejecutarlo, lo que mejora el rendimiento.
- **Máquina Virtual de Python**: El bytecode compilado se ejecuta en la Máquina Virtual de Python (Python Virtual Machine – PVM), que es una abstracción que hace que el código de Python sea portable y se pueda ejecutar en cualquier sistema operativo donde el intérprete esté disponible.

El intérprete de Python es una herramienta poderosa y flexible que hace que el lenguaje sea accesible y eficiente para una amplia variedad de aplicaciones de programación. Comprender cómo funciona el intérprete es fundamental para cualquier programador que desee dominar Python.


---

**Python 2 y Python 3** son dos versiones del lenguaje de programación Python, cada una con sus propias características y diferencias clave. PIP2 y PIP3 son las herramientas de gestión de paquetes correspondientes a cada versión, utilizadas para instalar y administrar bibliotecas y dependencias.

**Python 2 vs Python 3:**

- **Sintaxis de print**: En Python 2, ‘print’ es una declaración, mientras que en Python 3, ‘print()’ es una función, lo que requiere el uso de paréntesis.
- **División de enteros**: Python 2 realiza una división entera por defecto, mientras que Python 3 realiza una división real (flotante) por defecto.
- **Unicode**: Python 3 usa Unicode (texto) como tipo de dato por defecto para representar cadenas, mientras que Python 2 utiliza ASCII.
- **Librerías**: Muchas librerías populares de Python 2 han sido actualizadas o reescritas para Python 3, con mejoras y nuevas funcionalidades.
- **Soporte**: Python 2 llegó al final de su vida útil en 2020, lo que significa que ya no recibe actualizaciones, ni siquiera para correcciones de seguridad.

**PIP2 vs PIP3:**
- **Gestión de paquetes**: PIP2 y PIP3 son herramientas que permiten instalar paquetes para Python 2 y Python 3, respectivamente. Es importante usar la versión correcta para garantizar la compatibilidad con la versión de Python que estés utilizando.
- **Comandos de instalación**: El uso de pip o pip3 antes de un comando determina si el paquete se instalará en Python 2 o Python 3. Algunos sistemas operativos pueden requerir especificar pip2 o pip3 explícitamente para evitar ambigüedades.
- **Ambientes virtuales**: Es una buena práctica usar ambientes virtuales para mantener separadas las dependencias de proyectos específicos y evitar conflictos entre versiones de paquetes para Python 2 y Python 3.

La transición de Python 2 a Python 3 ha sido significativa en la comunidad de desarrolladores de Python, y es fundamental que los programadores comprendan las diferencias y sepan cómo trabajar con ambas versiones del lenguaje y susherramientas asociadas.

---