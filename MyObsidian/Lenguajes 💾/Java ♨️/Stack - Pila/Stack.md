Una *pila o stack* es una colección de objetos que se insertan y eliminan según el principio (LIFO) Last-in, First-out. Un usuario puede insertar objetos en una pila en cualquier momento. Pero sólo puede acceder o eliminar el objeto insertado más recientemente que permanezca (en la parte superior de la pila). 

Formalmente, una pila es un *tipo de datos abstracto (ADT)* que admite los dos métodos de actualización siguientes:
- **push(e):** Añade el elemento e a la parte superior de la pila.
- **pop( ):** Elimina y devuelve el elemento superior de la pila (o null si la pila está vacía).

Además, una pila admite los siguientes métodos de acceso para mayor comodidad:
- **top( )**: Devuelve el elemento superior de la pila, sin eliminarlo (o null si la pila está vacía).
- **size( ):** Devuelve el número de elementos de la pila.
- **isEmpty( ):** Devuelve un booleano que indica si la pila está vacía.
Por convención, asumimos que los elementos añadidos a la pila pueden tener un tipo arbitrario y que una pila recién creada está vacía.

