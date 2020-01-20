> Generar el jar, para ello debemos estar el raiz del proyecto
``` shell
#Mac
./mvnw clean package
#Windows
.\mvnw clean package

#Si queremos ponerlo en la carpera .M2 debemos de utilizar el instal
./mvnw clean install

# IMPOTANTE
# si queremos saltarnos el test y evitar tener problemas con servicios que no se estan ejecutando como
# base de datos debemos de hacer lo siguiente
./mvnw clean package -DskipTests
```

