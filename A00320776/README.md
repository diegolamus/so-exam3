
# Solución examen 3

**Nombre:** Diego Lamus  
**Código:** A00320776  

# Desarrollo  

**1.** Primero se instalaron y crearon las dependencias necesarias. Se instaló consuld, flask, python,  y se creo un script de python llamado microservice_a. Luego, Se abrieron los puertos necesarios para el correcto funcionamiento de los servicios.  

Al terminar los paso anteriores se creó un archivo de configuración para correr el microservicio. Para esto se ejecuto el siguiente comando:  

    echo '{"service": {"name": "microservice-a", "tags": ["flask"], "port": 8080,
    "check": {"script": "curl localhost:8080/health >/dev/null 2>&1", "interval": "10s"}}}' >/etc/consul.d/microservice-a.json  
    
El comando anterior crea un servicio llamado microsercive-a, que funciona en el puerto 8080, y le agrega un healthcheck que verifica continuamente si el microservicio se encuentra activo. Esto se guarda en /etc/consul.d/microservice-a.json.  

Luego, al correr el consul agent en modo cliente se puede evidenciar el funcionamiento de todo lo anterior, como se observa en las siguientes imagenes:  


![](https://github.com/diegolamus/so-exam3/blob/A00320776/solucion/A00320776/imagenes/Discovery%20Sevice.png)  

En la imagen anterior se observa como se inicia el consul agent en una screen.  

![](https://github.com/diegolamus/so-exam3/blob/A00320776/solucion/A00320776/imagenes/Microservicio%20funcionando.png)  

En la imagen anterior se observa el healthcheck que el consul agent realiza sobre el microservice_a  

**2.** Tras haber realizado la configuración del microservicio y haberlo agregado al consul agent se procede a unir el microservicio a un discovery service el cual fue montado por uno de nuestros compañeros. Para realizar esto se ejecuta el siguiente comando:  

     consul join 192.168.104.30  //ip del dispositivo que contiene el discovery service.  
     
Para ver si el consul join funciono correctamente se miran los miembros del consul con el comando "consul members" lo cual despliega lo siguiente:  
 
 
![](https://github.com/diegolamus/so-exam3/blob/A00320776/solucion/A00320776/imagenes/consul%20join.png)  

Como se observa en la imagen, entre los nodos del consul se encuentra un nodo agent-server, en tipo server, el cual corresponde al discovery service. Ademas se encuentran varios nodos en estado cliente, entre ellos el nodo A003207762 el cual corresponde al servicio que se montó en el punto 1. Si se observa con mas detalle el nodo en cuestión es de tipo cliente, se encuentra activo, y se encuentra en la ip 192.168.104.40, lo cual corresponde con la configuración que se le dio.  

**3.** A continuación se realizan algunas consultas al discovery service, como se observa en la imagen a continuación:  


![](https://github.com/diegolamus/so-exam3/blob/A00320776/solucion/A00320776/imagenes/consultas%20al%20discovery%20service.png)  

**a.** La primera consulta se hace a los microservicios que estan en estado critico, responde enviando la información del agente en modo servidor.  

**b.** En la segunda consulta se quiere ver el catalogo de servicios, y la respuesta indica que existen 4 microservicios, lo cual corresponde a los 4 agentes en modo cliente que se encuentran activos. Los respuesta indica que los nombres de los servicios son los siguientes:  
     
     consul
     microservice
     microservice-a
     microservice_a   
     
**c.** Finalmente se hace una consulta al microservice_a, y la respuesta brinda toda la información del microsrvicio (ip, tags, puerto...).
     



