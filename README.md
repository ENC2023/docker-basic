# Fundamentos de Docker

Docker es una plataforma para el desarrollo de aplicaciones contenirizadas, estandar de facto para la implementación de soluciones en la nube y base para la implementación de DevOps

* [Conceptos generales](https://github.com/ENC2023/docker-basic/blob/main/Fund-Docker.pdf)

# Bootcamp - Comandos fundamentales
```
REGISTROS
=========
Docker Hub: hub.docker.com
Docker registry : docker.io

0.- IMAGEN VS CONTENEDOR
------------------------

IMAGEN: Aplicacion organizada por capas de una aplicacion. No es ejecutable per-se.
CONTENEDOR: Ambiente de ejecucion de una imagen.

** Todo lo que hay en Docker Hub son imagenes (no contenedores)
** Se descarga la imagen al localhost. Al ejecutarse, se levanta un contenedor.


1.-EJECUTAR UN CONTENEDOR DESDE DOCKER HUB
------------------------------------------

* Busca la imagen local para ejecutarla. Si no la encuentra la carga desde
  el Docker Hub y levanta el contenedor de la imagen descargada:

Ej.-

docker run -e POSTGRES_PASSWORD=password postgres:9.6
docker ps

docker run -e POSTGRES_PASSWORD=password postgres:10.10
docker ps

2.-TRANSFIRIENDO UNA IMAGEN DEL DOCKER HUB AL LOCALHOST
-------------------------------------------------------
* Descarga la imagen del Docker Hub al Localhost

docker pull <image>

Ej.-
docker pull redis
docker images

docker run redis
docker ps

3.-CONSULTANDO LAS IMAGENES LOCALES
-----------------------------------
* Cada imagen tiene una version

docker images

4.-CONSULTANDO CONTENEDORES EN EJECUCION
----------------------------------------
docker ps

5.- EJECUTAR UN CONTENEDOR EN MODO DESCONECTADO
-----------------------------------------------
* Levanta el contenedor y regresa el control a la terminal

docker run -d <image>

Ej.- Parando el servidor redis conectado a la terminal y levantando de nuevo desconectado a la terminal

<Ctrl+C>    # Detiener el servidor redis que está corriendo conectado a la terminal

docker run -d redis   # Ejecutar el servidor redis desconectado de la terminal
docker ps

6.-DETENER UN CONTENEDOR
------------------------
* Se desea detener un contenedor que esta en ejecucion

Contenedor activo->Contenedor parado

docker stop <container-id>

Ej.- Se consulta el CONTAINER-ID del contenedor que se desea parar (hacerlo con redis):

docker ps
docker stop 8381867

docker ps

7.-REINICIAR UN CONTENEDOR
--------------------------
* Se desea reiniciar un contenedor anteriormente detenido

contenedor parado->contenedor reiniciado

docker start <CONTAINER-ID>

Ej.- Consultar el CONTAINER-ID del contenedor parado y volver a levantar

docker ps -a    # Muestra todos los contenedores activos y parados
docker start 8381867

docker ps       # Muestra solo los contenedores activos

8.-MOSTRAR LOS CONTENEDORES CORRIENDO Y PARADOS
-----------------------------------------------
docker ps -a

9.-VINCULANDO PUERTOS DEL HOST A PUERTOS DEL CONTENEDOR P/COMUNICACION CON EL EXTERIOR
--------------------------------------------------------------------------------------
* Asi el contenedor se puede usar por otro equipo/app a traves del puerto del localhost

docker run -p <localport>:<container-port>

Ej.- Supongo que se desea levantar otro servidor Redis, vinculando sus puertos del 
contenedor con puertos del host

docker stop 1980cbec25d3        # Deteniendo el primer servidor redis

docker run -p6000:6379 -d redis
docker run -p6001:6379 -d redis:4.0

docker ps

10.-CORRER UN CONTENEDOR Y DARLE UN NOMBRE
------------------------------------------
docker run --name <NOMBRE> 

Ej.- Deteniendo servidores redis actuales y levantando de nuevo con nombre

docker stop e1ff0978240d
docker stop c3a5b448e048

docker run -p6000:6379 -d --name redis-latest redis
docker run -d -p6001:6379 --name redis-older redis:4.0

docker ps

11.-DEPURANDO CONTENEDORES
--------------------------
docker exec -it <CONTAINER-ID> /bin/bash

Ej.- Entrar a un contenedor y revisar su sistema de archivos y ejectuar algunos comandos Linux

ls
pwd
env
exit

12.-REVISAR LA BITACORA (LOG) DE LA EJECUCION DE UN CONTENEDOR
---------------------------------------------------------------
* Porque quiza no corre bien, ha fallado, etc

docker logs <container-id>

Ej.- Revisando la bitácora del contenedor

docker logs redis-latest
docker logs redis-older

13.-EJECUTAR LA TERMINAL DEL CONTENEDOR
---------------------------------------

docker exec -it <container-id/container-name> /bin/bash (o bien) /bin/sh

docker exec -it ca903 /bin/bash
docker exec -it ca903 /bin/sh

-it -> interactive terminal

#exit -> salir de la terminal del contenedor

14.- PUBLICANDO LA IMAGEN A DOCKER HUB
--------------------------------------
Construyendo imagen local Docker. Ejecutar este comando en el directorio donde se encuentra el archivo DOCKERFILE:

docker build -t japp .

Levantando el contenedor Docker a partir de la imagen creada localmente

docker run japp

Subiendo la imagen al Docker Hub

docker tag local-image:tagname new-repo:tagname
docker push new-repo:tagname

** Ejemplo:
docker tag japp:latest ricardoqm/calculadora:latest
docker push ricardoqm/calculadora:latest

Levantando el contenedor Docker a partir de la imagen disponible en Docker Hub

docker run ricardoqm/calculadora:latest
```
