# ***Sticky Bit***
Cuando se establece el sticky bit en un directorio, indica al sistema operativo que solo el propietario del archivo, el propietario del directorio y el superusuario tienen permiso para eliminar o renombrar archivos dentro de ese directorio, incluso si otros usuarios tienen permisos de escritura en ese directorio.

Para establecer el sticky bit en un directorio en Linux, puedes utilizar el comando `chmod` con la notación numérica. El número asociado con el sticky bit es 1. Por lo tanto, para establecer el sticky bit, puedes usar el siguiente comando:

```bash
chmod +t nombre_directorio
```

Para ilustrar el concepto del sticky bit, supongamos que tienes un directorio compartido que es accesible para varios usuarios. Al establecer el sticky bit en ese directorio, aseguras que los usuarios puedan crear, modificar y eliminar archivos dentro del directorio, pero no podrán eliminar o renombrar archivos que no sean de su propiedad, a menos que sean el propietario del directorio o el superusuario.

El sticky bit es comúnmente utilizado en directorios de trabajo compartidos, como /tmp, para asegurar que los usuarios puedan crear y usar archivos temporales, pero no puedan eliminar archivos de otros usuarios en el mismo directorio.