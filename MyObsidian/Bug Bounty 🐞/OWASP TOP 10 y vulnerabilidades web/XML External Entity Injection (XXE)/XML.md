XML (eXtensible Markup Language) es un lenguaje de marcado diseñado para almacenar y transportar datos de forma estructurada y legible tanto por humanos como por máquinas. 

Las vulnerabilidades **XXE (XML External Entity)** aprovechan funcionalidades avanzadas del parser XML:

- **Entidades externas**: permiten incluir contenido de archivos locales o URLs externas.
    
- **DTD**: el parser XML lee definiciones de DTD para resolver esas entidades.
    

Si entiendes bien cómo se estructuran y procesan los documentos XML (etiquetas, entidades, DTD, namespaces), podrás ver cómo un atacante inyecta una declaración como:

```xml
<!DOCTYPE persona [
  <!ENTITY secreto SYSTEM "file:///etc/passwd">
]>
<persona>
  <nombre>&secreto;</nombre>
</persona>

```

---

**DTD (Document Type Definition)**  
Un DTD es un **contrato** que define la “gramática” de tu XML: qué elementos están permitidos, en qué orden, qué atributos llevan, y qué entidades (incluso externas) pueden usarse. Hay dos modalidades:

1. **DTD interna**  
    Se incluye dentro del mismo documento XML, justo después de la línea `<?xml …?>`:
    
    ```xml
    <?xml version="1.0"?>
    <!DOCTYPE libro [
      <!ELEMENT libro (título, autor, año)>
      <!ELEMENT título (#PCDATA)>
      <!ELEMENT autor (#PCDATA)>
      <!ELEMENT año (#PCDATA)>
    ]>
    <libro>
      <título>La Odisea</título>
      <autor>Homero</autor>
      <año>–800</año>
    </libro>
    ```
    
2. **DTD externa**  
    Se referencia mediante una URL o ruta a un archivo .dtd:
    
    ```xml
    <!DOCTYPE libro SYSTEM "http://midominio.com/libro.dtd">
    <libro> … </libro>
    ```
    
    Y en `libro.dtd` defines la gramática igual que en el ejemplo interno.
    

Con un DTD, al parsear en **modo de validación**, el parser:

- Comprueba que tu XML cumpla la estructura definida (elementos padre/hijo, orden, cardinalidad).
    
- Valida tipos simples (por ejemplo, que un campo sea `#PCDATA` vs. un elemento anidado).
    
- Resuelve **entidades** (internas o externas):
    
    ```xml
    <!ENTITY logo SYSTEM "http://midominio.com/logo.svg">
    ```
    
    Luego puedes usar `&logo;` dentro de tu XML para incluir ese contenido.
    

---

### ¿Por qué importa entender parseo y DTD antes de ver XXE?

Las vulnerabilidades XXE explotan la capacidad de los parsers XML de resolver entidades externas definidas en el DTD. Si el parser:

1. **Permite DTDs externas**
    
2. **Resuelve** entidades `SYSTEM` o `PUBLIC`
    
3. **Está en modo de validación** o acepta la carga de DTD
    

un atacante puede inyectar un DTD que lea archivos locales (`file://`) o haga peticiones a URLs arbitrarias, exponiendo datos sensibles.

---

¿Te gustaría un ejemplo práctico de cómo un DTD malicioso se inyecta en un XML para explotar XXE?