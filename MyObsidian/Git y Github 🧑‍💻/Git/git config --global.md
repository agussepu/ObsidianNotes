---
tags:
  - Git
---
---
Cada cosa que hagamos en git tendra una firma para saber quien hace cada cosa esta firma es nuestro alias y nuestro correo

```bash
# En este caso usaremos la configuracion global 
git config --global user.name "agussepu"

#Configuramos el email que se usara de manera global
git config --global user.email "elagussepulveda@gmail.com"

#con este comandos vemos la configuracion por defecto
$ git config --list

#de esta forma configuramos que el editor de codigo de git sea code y que ademas espere a cerrar el editor antes de guardar los cambios(--wait)
git config --global core.editor "code --wait"

#de esta forma las salidas en pantalla de git van a ser coloridas
git config --global color.iu true

#(solo windows, en linux usamos input en vez de true)con true agregamos el salto de linea automatico y cuando suba al servidor archivos borrara el r/n de win y lo pasa a /r/n de unix 
#en resumen con true le saca /r/n y lo deja en /n al subirlo y cuando lo bajamos le deja el /r/n
$ git config --global core.autocrlf true

#en linux usamos
$ git config --global core.autocrlf input
```