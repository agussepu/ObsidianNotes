Esas anotaciones son parte de la documentación de código en Java y se conocen como "Javadoc". Son comentarios especiales, pero tienen un propósito más allá de simplemente documentar el código para quien lo lee directamente.

Los comentarios Javadoc comienzan con `/**` y terminan con `*/`, y dentro de ellos puedes usar etiquetas como `@param` y `@return`.

Estas etiquetas:

1. **@param**: Documenta los parámetros de un método
    
    - Formato: `@param nombreDelParámetro descripción`
    - Describe qué es cada parámetro y qué valores se esperan
2. **@return**: Documenta el valor de retorno de un método
    
    - Formato: `@return descripción`
    - Describe qué devuelve el método

Aunque técnicamente son comentarios y no afectan la ejecución del código, tienen estos beneficios:

- **Generación de documentación**: Con la herramienta Javadoc, puedes generar automáticamente documentación HTML basada en estos comentarios
- **Ayuda en IDEs**: Los entornos de desarrollo como Eclipse, IntelliJ o NetBeans muestran esta información al pasar el cursor sobre un método
- **Estándar en equipos**: Proporcionan una forma estándar de documentar el código que otros desarrolladores esperan encontrar

Otras etiquetas comunes de Javadoc incluyen:

- `@author`: El autor del código
- `@version`: La versión del código
- `@throws` o `@exception`: Documenta excepciones que puede lanzar el método
- `@see`: Referencias a otros métodos o clases relacionados
- `@since`: Indica desde qué versión existe este elemento

Es una buena práctica incluirlos en tu código, especialmente cuando trabajas en equipos o desarrollas bibliotecas que serán utilizadas por otros.