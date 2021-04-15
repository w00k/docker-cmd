# Comandos básicos

Ver el historico de las imagenes 

```bash
docker ps -a 
```

Ver los contenedores en ejecución

```bash
docker ps
```

Correr una imagén.
* nombre-contenedor : nombre del contenedor
* hello-world : imagen a ejecutar

```bash
docker run --name nombre-contenedor hello-world
```

Cambiar el nombre del contenedor
* nombre-contenedor : nombre actual de contenedor
* hello-platzi : nombre nuevo del contenedor

```bash
docker rename nombre-contenedor hello-platzi
```

Eliminar contenedor

```bash
docker rm nombre/ID
```

Limpiar el hisorico de contenedores

```bash
docker container prune
```

Ejecutar un contendor
* -it : modo interactivo

```bash
docker run -it imagen
```

Ejecuta la imagen de ubuntu, sino existe, la descarga. La ejecución del contenedor se detiene, porque no tiene ninguna instrucción

```bash
docker run ubuntu
```

Ejecutar ubuntu en modo background
* --name : nombra el contenedor alwaysup
* -d : ejecuta en modo background
* tail -f /dev/null : ejecuta un comando

```bash
docker run --name alwaysup -d ubuntu tail -f /dev/null
```

Ingresar al contenedor en ejecución

```bash
docker exec -it alwaysup bash
```

Obtener pid del proceso, solo en Linux

```bash
docker inspect --format {{.State.Pid}} lawaysup
```

Detener un contenedor

```bash
docker stop alwaysup
```

Detener y borrar contenedor

```bash
docker rm -f alwaysup
```

## Exponer contenerdores

Docker posee su propio stack de networking, para exponer el contenedor
* --name : nombre del contenedor
* -p : publish, publica en puerto_local:puerto_interno_imagen

```bash
docker run --name proxy -p 8080:80 nginx
```

Exopner un contenedor en background 
* --name : nombre del contenedor
* -d : ejecución en background
* -p : publish, publica en puerto_local:puerto_interno_imagen

```bash
docker run --name proxy -d -p 8080:80 nginx
```

Ver los logs vivos

```bash
docker logs --f proxy
```

Ver los últimas 10 líneas

```bash
docker logs -tail 10 proxy
```

## Bind mount 

Correr mongo con nombre db

```bash
docker run -d --name db mongo
```

Montar una imagen, compartiendo carpeta local

```bash
docker run -d --name db -v local_path:path_imagen mongo
```

## Volumenes

Crear un volumen

```bash
docker volume create dbdata
```

Ver los volumenes creados

```bash
docker volume ls
```

Ejecutar un contenedor usando un volumen específico

```bash
docker run -d --name db --mount src=dbdata,dst=/data/db
```

## Coapiar archivos

Copiar archivo local en el contenedor

```bash
docker cp archivo_local contenedor:/ruta_en_el_contenedor
```

Copiar archivo del contenedor al ambiente local

```bash
docker cp contenedor:/ruta_en_el_contenedor ruta_local
```

Nota: los volumenes tmpfs, son para archivos que no persisten ó no nos interesa conservar