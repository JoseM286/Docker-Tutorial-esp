# Docker: Comandos básicos

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

## 13) Redes en Docker

### Tipos de redes y segregación en Docker
Docker permite la creación de redes para que los contenedores se comuniquen entre sí o estén aislados de otros.

#### a) Comandos para gestionar redes en Docker
```sh
docker network # Ver comandos de redes en Docker
```

#### b) Crear una red en Docker
```sh
docker network create mi-red
```

#### c) Especificar el driver de red al crear una red
```sh
docker network create --driver bridge mi-red
```

##### i) Tipos de drivers de redes en Docker:
1. **Bridge**: Red por defecto que permite la comunicación entre contenedores en el mismo host.
2. **Host**: Los contenedores comparten la red del host (puede implicar riesgos de seguridad).
3. **Overlay**: Permite la comunicación entre contenedores en diferentes hosts.
4. **Macvlan**: Asigna una dirección MAC a un contenedor, funcionando como un dispositivo físico.
5. **None**: El contenedor no tiene acceso a la red.

#### d) Ver lista de redes en Docker
```sh
docker network ls
```

#### e) Inspeccionar una red específica
```sh
docker network inspect mi-red
```

#### f) Conectar un contenedor a una red específica al iniciarlo
```sh
docker run -d --name mi-contenedor --network mi-red nginx
```

#### g) Conectar un contenedor existente a una red existente
```sh
docker network connect mi-red mi-contenedor
```

#### h) Desconectar un contenedor de una red
```sh
docker network disconnect mi-red mi-contenedor
```

#### i) Eliminar una red en Docker
```sh
docker network rm mi-red
```

#### j) Eliminar todas las redes inactivas (excepto bridge, host y none)
```sh
docker network prune
```

---
