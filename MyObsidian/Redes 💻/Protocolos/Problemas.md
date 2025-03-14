PHP en Arch El mensaje indica que Apache está ejecutando un **MPM (Multi-Processing Module) basado en hilos**, probablemente `event` o `worker`, mientras que el módulo PHP instalado no es **thread-safe**. Esto ocurre porque el módulo PHP para Apache (`libphp.so`) necesita ser compatible con el MPM utilizado.

### **Soluciones posibles**

#### **1. Cambiar a MPM `prefork`**

El MPM `prefork` utiliza procesos en lugar de hilos, por lo que no requiere que PHP sea thread-safe.

1. **Edita la configuración de Apache**:
    
    bash
    
    Copiar código
    
    `sudo nano /etc/httpd/conf/httpd.conf`
    
2. Busca y asegúrate de cargar el módulo `prefork` en lugar de `event` o `worker`:
    
    apache
    
    Copiar código
    
    `LoadModule mpm_prefork_module modules/mod_mpm_prefork.so`
    
3. Asegúrate de que no estén cargados los módulos `mpm_event` o `mpm_worker`. Comenta cualquier línea que los cargue:
    
    apache
    
    Copiar código
    
    `# LoadModule mpm_event_module modules/mod_mpm_event.so # LoadModule mpm_worker_module modules/mod_mpm_worker.so`
    
4. Guarda y cierra el archivo.
    
5. Reinicia Apache:
    
    bash
    
    Copiar código
    
    `sudo systemctl restart httpd`
    

Esto suele ser suficiente para resolver el problema sin necesidad de recompilar PHP.