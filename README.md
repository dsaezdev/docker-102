# Laboratorio Docker Compose

Este laboratorio se basa en el mismo ejercicio que corrimos en Replit con Python y Flask.

## Preparación

Haz un fork de este repo.

Clona el fork en tu pc.

## Paso 1

Ejecuta `docker init`.

Selecciona Python como el `application platform`.

Cuando aparezca la pregunta `What is the command to run your app?`, escribe `python main.py`.

Abre el archivo `compose.yaml`, en la línea 16, debajo de la sección `ports` agrega estas líneas:

```
    enviroment:
      - PORT
      - HOST
      - DB
      - DB_USERNAME
      - DB_PASSWORD
```

Asegurate que `ports` y `enviroment` estén alineados en la misma columna.

Revisa el archivo `.env`, configura las variables con los valores que usaste en el ejercicio en Replit (es decir, usa las credenciales de ElephantSQL).

Levanta la aplicación con el siguiente comando:

```
docker compose up --build
```

Revisa que todo está bien navegando a la dirección `localhost:8000`.

### Preguntas

¿Qué pasa si cambias el valor de la variable PORT?
No se puede acceder desde afuera a la pagina al nuevo puerto, pero sigue arriba en el puerto antiguo.
¿Qué cambios debes hacer para cambier el port a 8080?
cambiar en el archivo .env y en el compose.yaml

## Paso 2

Deten `docker compose` presionando `control-c`.

Elimina los comentarios a partir de la línea 28.

Asegurate de crear un archivo en la carpeta `db` llamado `password.txt`, coloca en este una clave cualquiera.

Modifica el archivo `.env` para que se pueda conectar al servicio `db`.

Tips: 
  - El valor para `HOST` es `db`
  - los valores que necesitan están declarados en la definición del servicio, debes hacer el "match" de las variables allí definidas con las que necesitas.

Esta vez ejecuta el comando `docker compose` de este modo:

```
docker compose up -d --build 
```

La opción `-d` permite dejar ejecutando los servicios y libera la consola.

### Actividades

Ejecuta `docker ps`. 

¿Qué obtienes?.
CONTAINER ID   IMAGE               COMMAND                  CREATED          STATUS                          PORTS                                                  NAMES
c23c33060840   docker-102-server   "/bin/sh -c 'python …"   51 seconds ago   Up 37 seconds                   8000/tcp, 0.0.0.0:8080->8080/tcp                       docker-102-server-1
05e0f92726c7   postgres            "docker-entrypoint.s…"   51 seconds ago   Up 48 seconds (healthy)         5432/tcp                                               docker-102-db-1
e0bdbf0b9945   mongo:latest        "docker-entrypoint.s…"   3 months ago     Up 47 hours                     0.0.0.0:27017->27017/tcp                               docker-compose-mongodb-1
0f73473aee0a   mysql:latest        "docker-entrypoint.s…"   3 months ago     Up 47 hours                     0.0.0.0:3306->3306/tcp, 33060/tcp                      docker-compose-mysql-1
a550cd51b3e9   bitnami/kafka       "/opt/bitnami/script…"   3 months ago     Restarting (1) 44 seconds ago                                                          docker-compose-kafka-1
c2ed4c763f13   bitnami/zookeeper   "/opt/bitnami/script…"   3 months ago     Up 47 hours                     2888/tcp, 3888/tcp, 0.0.0.0:2181->2181/tcp, 8080/tcp   docker-compose-zookeeper-1

Ejecuta `docker images`. 

¿Cuál es el tamaño de la imagen del servidor flask?
140MB

¿Cuál es el tamaño de la imagen postgres?
 417MB

¿Cuándo fueron creadas cada una de las imágenes?
docker-102-server   latest    376d078cb885   51 minutes ago   140MB
postgres            latest    fbd1be2cbb1f   7 weeks ago      417MB

Ahora ejecuta `docker compose logs -f`, esto te permite revisar el log de los contenedores.

Si navegas hacia la aplicación (http://localhost:8000/) se produce un error, revisa el log.

¿Cuál es la causa del error?

Cierra el log presionando `control-c`, luego detén la aplicación con este comando:

```
docker compose down
```

