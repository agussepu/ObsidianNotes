# Linux
Habilidades básicas de Linux:**

#### **Comandos esenciales de la terminal:**

- Navegación por el sistema de archivos: `ls`, `cd`, `pwd`, `tree`.
- Gestión de archivos y directorios: `cp`, `mv`, `rm`, `mkdir`, `touch`.
- Visualización de archivos: `cat`, `less`, `more`, `head`, `tail`.
- Permisos de archivos: `chmod`, `chown`, `umask`.
- Comandos de búsqueda: `find`, `locate`, `grep`.

#### **Edición de texto desde la terminal:**

- Uso de editores como `vim`, `nano` o `emacs`.
- Realizar búsquedas y reemplazos en archivos.

#### **Gestión de usuarios y grupos:**

- Crear, modificar y eliminar usuarios: `useradd`, `usermod`, `userdel`.
- Gestión de grupos: `groupadd`, `groupmod`, `groupdel`.
- Configuración de permisos y acceso: `sudo`, `passwd`.

---

### **2. Administración de sistemas Linux:**

#### **Gestión de procesos y recursos:**

- Monitoreo de procesos: `ps`, `top`, `htop`, `kill`.
- Gestión de servicios: `systemctl`, `service`.
- Monitoreo del uso de disco y memoria: `df`, `du`, `free`.

#### **Gestión de paquetes:**
- Uso de gestores de paquetes según la distribución:
    - **Debian/Ubuntu:** `apt`, `dpkg`.
    - **Red Hat/CentOS:** `yum`, `dnf`, `rpm`.
    - **Arch Linux:** `pacman`.

#### **Tareas programadas:**

- Uso de `cron` para tareas periódicas.
- Uso de `at` para tareas puntuales.

#### **Gestión de logs:**

- Lectura y análisis de logs: `journalctl`, `/var/log/syslog`, `/var/log/messages`.
- Configuración básica de syslog para centralizar registros.

---

### **3. Redes en Linux:**

#### **Configuración y monitoreo:**

- Comandos básicos: `ip`, `ifconfig`, `ping`, `traceroute`, `netstat`, `ss`.
- Configuración de interfaces de red: edición de archivos en `/etc/network/` o `/etc/netplan/`.
- Diagnóstico de red: `tcpdump`, `nmap`, `nslookup`, `dig`.

#### **Seguridad de red:**

- Configuración de firewalls: `iptables`, `ufw`, `firewalld`.
- Configuración de SSH: `sshd_config`, generación de claves SSH con `ssh-keygen`.

---

### **4. Automatización y scripting:**

- Escritura de scripts básicos en Bash:
    - Uso de variables, bucles y condicionales.
    - Automatización de tareas repetitivas.
- Uso de herramientas como `awk`, `sed` y `grep` para procesar texto.
- Gestión de procesos y ejecución de tareas paralelas con `xargs`, `&`, `wait`.

---

### **5. Gestión de almacenamiento:**

- Montaje y desmontaje de sistemas de archivos: `mount`, `umount`.
- Configuración de particiones y discos: `fdisk`, `parted`, `lsblk`.
- Uso de sistemas de archivos: ext4, XFS, Btrfs.
- Gestión de volúmenes lógicos: `lvm`.

---

### **6. Seguridad en Linux:**

- Configuración de permisos avanzados con `ACL` (Access Control Lists).
- Configuración de políticas de contraseñas seguras: `pam.d`.
- Configuración de SELinux o AppArmor (según la distribución).
- Auditorías de seguridad básicas con herramientas como `auditd`.

---

### **7. Trabajo con servidores Linux:**

- **Servidor web:** Configuración de Apache o Nginx.
- **Servidor SSH:** Configuración segura, cambio de puertos, autenticación por clave.
- **Servidor de base de datos:** Instalación y configuración de MySQL, PostgreSQL o MariaDB.

---

### **8. Virtualización y contenedores:**

- Uso de máquinas virtuales con `KVM` o `VirtualBox`.
- Uso de contenedores con `Docker` y orquestadores como `Kubernetes`.

---

### **9. Monitoreo y diagnóstico:**

- Uso de herramientas como `Nagios`, `Zabbix` o `Prometheus` para monitorear servidores.
- Configuración básica de scripts de alerta.

---

### **10. Documentación y buenas prácticas:**

- Saber cómo escribir documentación clara y reproducible.
- Usar control de versiones como Git para scripts y configuraciones.