
# Solución examen 3

**Nombre:** Diego Lamus  
**Código:** A00320776  

# Desarrollo  

Primero se instalaron y crearon las dependencias necesarias. Se instalo consuld, flask, python,  y se creo un script de python llamado microservice_a. Luego, Se abrieron los puertos necesarios para el correcto funcionamiento de los servicios.  

Al terminar los paso anterior se creó un archivo de configuración para correr el microservicio. Para esto se ejecuto el siguiente comando:  

    echo '{"service": {"name": "microservice-a", "tags": ["flask"], "port": 8080,
    "check": {"script": "curl localhost:8080/health >/dev/null 2>&1", "interval": "10s"}}}' >/etc/consul.d/microservice-a.json  
    
El comando anterior crea un servicio llamado microsercive-a, que funciona en el puerto 8080, y le agrega un healthcheck que verifica continuamente si el microservicio se encuentra activo. Esto se guarda en /etc/consul.d/microservice-a.json.  

Luego, al correr el consul agent en modo cliene se puede evidenciar el funcionamiento de todo lo anterior, como se observa en las siguientes imagenes:  


![]()

