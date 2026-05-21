 # Contenedores de Sistemas gestores 

 ![ImagenDocker](./img/Gemini_Generated_Image_hki6rxhki6rxhki6.png)

 ## Comandos Docker con Descripcion
  | Comando | Descripcion |
  | :--- | :--- |
  | **docker --version** | _Verifica la version de docker_ |
  | **docker pull nombre_imagen**| _Descarga una imagen de Docker Hub_|
  [DockerHub](https://hub.docker.com/)
 | **docker images** | _Visualiza las imagenes_ |
 | **docker run** | _Crea un contenedor_ |
 | **docker ps** | _Visualiza todos los contenedores en ejecucion_ |
 | **docker ps -a** | _Visualiza todos los contenedores en ejecucion y no en ejecucion_ |
 | **docker container ls -a** | _Visualiza todos los contenedores en ejecucio_ |
 | **docker stop nombre_contenedor o ID** | _Detiene un contenedor_ |
 | **docker start nombre_contenedor o ID** | _Inicia un contenedor_ |
 | **docker rm nombre_contenedor o ID** | _Elimina un contenedor que no esta en ejecucion_ |
 | **docker rm -f nombre_contenedor o ID** | _Elimina un contenedor que no esta en ejecucion_ |
 | **docker volume ls** | _Lista los volumenes que tiene docker_ |
 | **docker volume create nombre_contenedor o ID** | _Crea un volumen |
 | **docker volume rm nombre_contenedor o ID** | _Elimina un volumen |

# Comandos de Contenedores de SGBD

 ```
 docker pull docker/getting-started
 ```

 ### Contenedor de tutorial de docker 

 ``` 
 docker run -d --name tutorial-docker -p 80:80  docker/getting-started:latest
 ```

 ### Contenedor de MariaDB sin volumen

 ```
 docker run -d --name server-MariaDBG3 -p 3342:3306 -e MARIADB_ROOT_PASSWORD=12345 70385
 ```

 
 ### Contenedor de MariaDB con volumen

 ```
 ```
docker run -d --name server-MariaDBG3 \
-p 3342:3306 -e MARIADB_ROOT_PASSWORD=12345 \
-v vol-mariadbg3:/var/lib/mysql 70385

 ### Contenedor de postgres con volumen

 ```docker

docker run -d --name server-postgresg3 \
-e POSTGRES_PASSWORD-123456 \
-P 5456:5432 -v vol-postgresg3:/var/lib/postgresql/dat \
eba8d

```