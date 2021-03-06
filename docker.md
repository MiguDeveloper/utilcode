
# Comandos Docker

> Iniciar la configuración básica de un Dockerfile
``` properties 
FROM openjdk:8
VOLUME /tmp
EXPOSE 8888
ADD ./target/servicio-config-server-0.0.1-SNAPSHOT.jar config-server.jar
ENTRYPOINT ["java", "-jar", "/config-server.jar"]
```

> Creamos(Construir) la imagen: Ejecutar en la raiz del proyecto habiendo ya creado el Dockerfile: con 'build' generamos la imagen y con 't' indicamos el nombre y el tag para la categoria o versiones, no olvidar poner le '.'
```
docker build -t nombre_del_servicio:v1 .
```

> Verificamos que se haya generado la imagen
```
docker images
```

> Ahora levantamos(ejecutar la instancia) una instancia de la imagen, cuando el puerto es random tenemos que poner '-P'
```
docker run -p 8761:8761 --name servicio-eureka-server --network nombreDeLaRed servicio-eureka-server:v1
```

> IMPORTANTE: si ya tenemos ejecutando una instancia que tiene puerto random podemo levantar una nueva instancia facilmente
```
docker run -P --network springcloud servicio-productos:v1
```

> Comando para generar un red 
```
docker network create nombreDeLaRedaCrear
```

> listar los contenedores(instancias) que tenemos, dos comandos básicos
``` shell
docker container ls
docker ps
```
> listar los contenedores que estan detenidos
```
docker ps -a
```

> Ver el log 
```
docker logs -f CONTAINER_ID
```
> Reiniciar una imagene en: solo debemos de poner el nombre del contenedor si el tag de la version
```
docker restart NOMBRE_CONTEINER
```

> Para detener un servicio
```
docker stop CONTAINER_ID
```

> Si deseamos detener varios instancias con un solo comando
``` shell
# Nos permite ver los ID de los contenedores que estan en UP
docker ps -q

# Detener contenedores: Ahora para detener en grupo haremos lo siguiente
docker stop $(docker ps -q)

# Eliminar contenedores: Para remover en grupo
docker rm $(docker ps -aq)
```

> Para eliminar todas las imagenes
```
docker rmi $(docker images -aq)
```

> Para eliminar una instancia 
```
docker rm CONTAINER_ID
```

> Mostrar la version de docker-compose: nos sirve para componer contenedores de docker en un solo archivo, configurar nuestro despliegue
```
docker-compose --version
```

> Para ejecutar un docket compose
```
docker-compose up
```

> Para eliminar los contenedores que se estan ejecutando mediante docker-compose
```
docker-compose down -v
```

> Docker-compose: Cuando tenemos dependencias de servicios debemos de ejecutarlos en orden, se usa los names mas no los tags de versiones
``` shell
docker-compose up -d config-server
docker-compose up -d servicio-eureka-server
docker-compose up -d microservicios-mysql8

# Para ver el log de ejecucion de los comandos anteriores podemos ejecutar
docker-compose logs -f
```

> Para eliminar images
```
docker rmi CONTAINER_ID
```

> Descargar imagen docker
```
docker pull mysql:8
```
> Descargar imagen postgres
```
docker pull postgres:12-alpine
```
> Descargar rabbitMQ con version management
```
docker pull rabbitmq:3.8-management-alpine
```

> Para levantar el servicio de Rabbit debemos de levantar dos puertos la parte web y el broker, requiere dar un nombre tambien para relacionarlo e.g desde zipkin
```
docker run -p 15672:15672 -p 5672:5672 --name microservicios-rabbitmq38 --network springcloud -d rabbitmq:3.8-management-alpine
```

> Para levantar Zipkin
```
docker run -p 9411:9411 --name zipkin-server --network springcloud -e RABBIT_ADDRESSES=nombreMicroServicioRabbit:5672 -e STORAGE_TYPE=mysql -e MYSQL_USER=zipkin -e MYSQL_PASS=znfmdy -e MYSQL_HOST=nombreDelMicroservicioMysql zipkin-server:v1
```
> Para ver los detalles de un contenedor
```
docker inspect CONTAINER_ID
```

> Ejecutar la imagen de mysql: '-e' para setear una variable de entorno, '-d' para correr en background (en silencio! :D)
```
docker run -p 3306:3306 --name microservicios-mysql8 --network springcloud - e MYSQL_ROOT_PASSWORD=sasa -e MYSQL_DATABASE=db_springboot_cloud -d mysql:8
```

> Ejecutar la imagen de postgres: '-e' para setear una variable de entorno, '-d' para correr en background (en silencio! :D)
```
docker run -p 5432:5432 --name microservicios-postgres12 --network springcloud - e POSTGRES_PASSWORD=sasa -e POSTGRES_DB=db_springboot_cloud -d mysql:8
```