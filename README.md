#Proyecto Parcial Microservicios Cloud Computing


git clone repositorio

En EC2 MV BD
1. Crear bases de datos
Primero abrimos los puertos
IMAGEN mvDB-puertos

1.1 Microservicio 1
$ docker volume create mysql_data
$ docker run -d --rm --name mysql_c -e MYSQL_ROOT_PASSWORD=utec -p 8001:3306 -v mysql_data:/var/lib/mysql mysql:8.0

Para definir las tablas en cada base de datos, se puede acceder al contenedor mediante comandos o utilizando adminer
POR COMANDOS
$ docker exec -it mysql_c bash
$ mysql -u root -p
utec
y copiamos y pegamos micro1/schema.sql

POR ADMINER 
$ docker run -d --rm --name adminer_c -p 8080:8080 adminer
IMAGEN adminer-login-mysql
IMAGEN micro1-adminer

1.2 Microsevicio 2
$ docker volume create postgres_data
$ docker run -d --rm --name postgres_c -e POSTGRES_PASSWORD=utec -p 8002:5432 -v postgres_data:/var/lib/postgresql postgres
$ docker exec -it postgres_c bash
$ psql -U postgres -W
y copiamos y pegamos micro2/schema.sql

1.3 Microservicio 3
$ docker volume create mongo_c
$ docker run -d --rm --name mongo_c -p 27017:27017 -v mongo_data:/data/db mongo:latest
$ docker exec -it mongo_c bash
$ mongosh

3. Correr contenedores en 2 MV Prod
docker run -d --rm --name mysql_c -p 8001:8001 sofk/microservicio1
docker run -d --rm --name postgres_c -p 8002:8002 sofk/microservicio2
docker run -d --rm --name mongo_c -p 8003:8003 sofk/microservicio3
