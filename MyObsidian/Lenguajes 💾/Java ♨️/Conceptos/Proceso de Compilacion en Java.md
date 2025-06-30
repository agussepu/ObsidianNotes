***Proceso de Compilación***
Java es tanto compilado como interpretado, lo que se conoce como un enfoque híbrido:
1. **Fase de compilación**:
    - Tu código fuente Java se compila a bytecode
    - El bytecode no es código máquina específico para ningún procesador
    - Es un conjunto de instrucciones diseñado para la JVM
2. **Fase de interpretación/ejecución**:
    - La JVM lee e interpreta el bytecode
    - Lo traduce a instrucciones nativas para el hardware específico donde se ejecuta

Esta arquitectura híbrida es lo que permite la característica "write once, run anywhere" (escribe una vez, ejecuta en cualquier parte) de Java:

- El mismo bytecode puede ejecutarse en cualquier plataforma que tenga una JVM
- No necesitas recompilar tu código para diferentes sistemas operativos
- La JVM actúa como una capa de abstracción entre tu programa y el hardware

Los programas Java atraviesan **cinco fases** 
- **Edit** (Edición): El programador escribe programas usando un editor, almacena el programa en disco con extensión de nombre .java -
- **Compile** (Compilación): Se usa javac (el compilador Java) para crear “bytecodes” desde el código fuente del programa; bytecodes son almacenados en archivos .class
- **Load** (Carga): El cargador de Clases lee los bytecodes del archivo .class poniéndolo en memoria
- **Verify** (Verificación): El verificados de Bytecode examina los bytecodes para asegurarse que ellos sean válidos y que no violen las restricciones de seguridad
- **Execute** (Ejecución): Java Virtual Machine (JVM) usa una combinación de interpretación y compilación “just-in-time” para traducir los bytecodes a lenguaje de máquina