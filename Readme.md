# Docker

## 1) Sistema de contenedores más popular
Docker permite realizar pruebas o test en diferentes máquinas de forma consistente.

### Características:
- Es similar a una máquina virtual, pero sin su propio sistema operativo.
- Usa una parte aislada del sistema operativo.

---

## 2) Tipos de Docker

### a) Docker Desktop
- Sin restricción de licencia.
- Trabaja sobre una máquina virtual de Linux.
- Disponible para Windows.
- Tiene interfaz visual.

### b) Docker Engine
- Funciona directamente sobre Linux.

---

## 3) Partes de Docker

### a) Docker Hub
- Repositorio de imágenes Docker.

### b) Dockerfile
- Archivo de texto que contiene las instrucciones para construir una imagen.

### c) Imagen
- Archivo binario con todo lo necesario para ejecutar un contenedor.
- Es una plantilla para crear instancias (contenedores).

### d) Contenedor
- Instancia en ejecución de una imagen.
- Proceso que se ejecuta en un entorno aislado.
- Contiene una aplicación y sus dependencias.

---

## 4) Comandos de activación e información de contenedores

```sh
docker run <image>          # Activa un contenedor o descarga la imagen si no la tiene
docker run -d <image>       # Activa el contenedor en segundo plano
docker run --name <name> <image> # Asigna un nombre al contenedor
docker ps                  # Muestra los contenedores activos
docker ps -a               # Muestra los contenedores activos e inactivos
docker logs <id>           # Muestra logs del contenedor
docker logs -f <id>        # Muestra logs en tiempo real
docker start -ai <id>      # Reactivar un contenedor en modo interactivo
docker start <id>          # Reactivar un contenedor sin modo interactivo
```

---

## 5) Comandos de gestión de contenedores

```sh
docker exec <id> <comando>     # Ejecutar un comando dentro del contenedor
docker exec -it <id> bash      # Acceder al contenedor en modo interactivo con bash
docker rm <id>                 # Eliminar un contenedor si no está activo
docker rm -f <id>              # Forzar la eliminación de un contenedor activo
docker container prune         # Borrar todos los contenedores detenidos
```

---

## 6) Comandos de imágenes

```sh
docker pull <image>        # Descargar una imagen
docker images              # Mostrar las imágenes disponibles
docker rmi <image>         # Borrar una imagen si no tiene un contenedor asociado
docker rmi -f <image>      # Forzar el borrado de una imagen
docker image prune         # Borrar imágenes sin contenedores asociados
docker search <image>      # Buscar una imagen en Docker Hub
```

---

## 7) Dockerfile - Instrucciones básicas

```Dockerfile
FROM <imagen_base>  # Define la imagen base
RUN <comando>       # Ejecuta un comando en la imagen
COPY <origen> <destino>  # Copia archivos del host a la imagen
WORKDIR <directorio>  # Define el directorio de trabajo\CMD ["comando"]  # Comando por defecto al iniciar el contenedor
ENTRYPOINT ["comando"]  # Comando obligatorio al iniciar el contenedor
```

---

## 8) Crear una imagen desde un Dockerfile

```sh
docker build -t <nombre_imagen> .  # Crear una imagen en el directorio actual
docker run -d --name <nombre_contenedor> -p 8080:80 <nombre_imagen>  # Crear y ejecutar el contenedor
docker tag <nombre_imagen>:latest usuario/<nombre_imagen>:latest  # Etiquetar imagen para Docker Hub
docker push usuario/<nombre_imagen>:latest  # Subir imagen a Docker Hub
```

---

## 9) Volúmenes en Docker

```sh
docker volume create mi-volumen           # Crear un volumen
docker volume ls                          # Listar volúmenes
docker volume inspect mi-volumen          # Inspeccionar un volumen
docker run -d --name mi-contenedor -v mi-volumen:/datos nginx  # Montar un volumen en un contenedor
docker volume rm mi-volumen               # Eliminar un volumen
docker cp archivo.txt mi-contenedor:/datos/archivo.txt  # Copiar archivo al contenedor
docker cp mi-contenedor:/datos/archivo.txt archivo.txt  # Copiar archivo del contenedor al host
```

---

## 10) Redes en Docker

```sh
docker network create mi-red        # Crear una red
```

---
