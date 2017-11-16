
# Solución examen 3

**Nombre:** Diego Lamus  
**Código:** A00320776  

# Desarrollo  

*1.* Primero se instalaron y crearon las dependencias necesarias. Se instalo consuld, flask, python,  y se creo un script de python llamado microservice_a. Luego, Se abrieron los puertos necesarios para el correcto funcionamiento de los servicios.  

Al terminar los paso anterior se creó un archivo de configuración para correr el microservicio. Para esto se ejecuto el siguiente comando:  

    echo '{"service": {"name": "microservice-a", "tags": ["flask"], "port": 8080,
    "check": {"script": "curl localhost:8080/health >/dev/null 2>&1", "interval": "10s"}}}' >/etc/consul.d/microservice-a.json  
    
El comando anterior crea un servicio llamado microsercive-a, que funciona en el puerto 8080, y le agrega un healthcheck que verifica continuamente si el microservicio se encuentra activo. Esto se guarda en /etc/consul.d/microservice-a.json.  

Luego, al correr el consul agent en modo cliene se puede evidenciar el funcionamiento de todo lo anterior, como se observa en las siguientes imagenes:  


![](https://github.com/diegolamus/so-exam3/blob/A00320776/solucion/A00320776/imagenes/Discovery%20Sevice.png)  

En la imagen anterior se observa como se inicia el consul agent en una screen.  

![](https://github.com/diegolamus/so-exam3/blob/A00320776/solucion/A00320776/imagenes/Microservicio%20funcionando.png)  

En la imagen anterior se observa el healthcheck que el consul agent realiza sobre el microservice_a  

*2.* Tras haber realizado la configuración del microservicio y haberlo agregado al consul agent se procede a unir el microservicio a un discovery service el cual fue montado por uno de nuestros compañeros




