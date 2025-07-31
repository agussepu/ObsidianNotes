---
tags:
  - BugBounty
---
---
# Dashboard
Primero debo aprender a hacer [[Reconocimiento]]

**Me voy a enfocar en las siguientes vulnerabilidades**
- XSS
- Broken Access Control / IDOR
- SSRF
- CSRF
- SQLi (Probablemente el mes que viene)
- Open Redirect
- CORS





---
### VM Fedora con QEMU
Finalmente encontré una solución. No era el kernel ni la configuración del bridge.

Resulta que, al tener una configuración basada en firewalld, libvirt esperaba que existiese una validación explicita para conectarse a la interfaz física, pero no funcionaba porque no había una autorización explicita del forwarding de IP, pese a que la regla estaba definida en sysctl. Libvirt tampoco tenia manera de validarlo, porque el servicio de firewall estaba desactivado. Por ello, y si a alguien le le sirve, lo que hice fue:

```bash
sudo firewall-cmd --permanent --direct --passthrough ipv4 -I FORWARD -i virbr0 -j ACCEPT

sudo firewall-cmd --permanent --direct --passthrough ipv4 -I FORWARD -o virbr0 -j ACCEPT

sudo firewall-cmd --reload
```
Desconozco qué directiva cambió en Fedora 41/firewalld-2.2.3 como para que esta regla sea necesaria, pero es la única forma en la que pude volver a habilitar el acceso a internet en la VMs.

