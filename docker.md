
# Comandos Docker

> Ejecutar en la raiz del proyecto habiendo ya creado el Dockerfile: con 'build' generamos la imagen y con 't' indicamos el nombre y el tag para la categoria o versiones, no olvidar poner le '.'
```
docker build -t config-server:v1 .
```

> Verificamos que se haya generado la imagen
```
docker images
```

> Comando para generar un red 
```
docker network create nombreDeLaRedaCrear
```

> listar los contenedores(instancias) que tenemos dos comandos basicos
``` shell
docker container ls

```