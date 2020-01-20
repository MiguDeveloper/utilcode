
# Comandos Docker

> Iniciar la configuración básica de un Dockerfile
``` properties 
FROM openjdk:8
VOLUME /tmp
EXPOSE 8888
ADD ./target/servicio-config-server-0.0.1-SNAPSHOT.jar config-server.jar
ENTRYPOINT ["java", "-jar", "/config-server.jar"]
```

> Construir la imagen: Ejecutar en la raiz del proyecto habiendo ya creado el Dockerfile: con 'build' generamos la imagen y con 't' indicamos el nombre y el tag para la categoria o versiones, no olvidar poner le '.'
```
docker build -t config-server:v1 .
```

> Verificamos que se haya generado la imagen
```
docker images
```

> Ahora levantamos(ejecutar la instancia) una instancia de la imagen, cuando el puerto es random tenemos que poner '-P'
```
docker run -p 8761:8761 --name servicio-eureka-server --network nombreDeLaRed servicio-eureka-server:v1
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
docker logs -f ID_DEL_CONTENEDOR
```
> Reiniciar una imagene en: solo debemos de poner el nombre del contenedor si el tag de la version
```
docker restart NOMBRE_CONTEINER
```

> Descargar imagen docker
```
docker pull mysql:8
```
> Descargar imagen postgres
```
docker pull postgres:12-alpine
```

> Ejecutar la imagen de mysql: '-e' para setear una variable de entorno, '-d' para correr en background (en silencio! :D)
```
docker run -p 3306:3306 --name microservicios-mysql8 --network springcloud - e MYSQL_ROOT_PASSWORD=sasa -e MYSQL_DATABASE=db_springboot_cloud -d mysql:8
```

> Ejecutar la imagen de postgres: '-e' para setear una variable de entorno, '-d' para correr en background (en silencio! :D)
```
docker run -p 5432:5432 --name microservicios-postgres12 --network springcloud - e POSTGRES_PASSWORD=sasa -e POSTGRES_DB=db_springboot_cloud -d mysql:8
```