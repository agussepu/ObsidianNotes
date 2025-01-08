En este caso vamos a traer un contenedor que tiene una vulnerabilidad por lo que lo haríamos con 

```bash
git clone https://github.com/vulhub/vulhub/tree/master/kibana/CVE-2018-17246
# Pero en este caso como solo queremos clonar la subcapeta que seria kibana/CVE-2018-17246, debemos hacer lo siguiente

svn checkout https://github.com/vulhub/vulhub/trunk/kibana/CVE-2018-17246

# Igual esto no me sirvio asi q lo descargue de aca https://download-directory.github.io
```

