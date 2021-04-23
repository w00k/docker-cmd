## Detener Contenedor

Para detener un contenedor se ejecuta stop, envía systerm y después kill

```bash
docker stop looper
```

Ver el último proceso, esté o no funcionando

```bash
docker ps -l 
```

Ejecutar un kill al contenedor, las peticioens que están procesando terminarán de procesar y posteriormente se apagará

```bash
docker kill looper 
```

Ver el process id del proceso en el contenedor

```bash
docker exec looper ps -ef
```

Cambiar el proceso a 1, formato exec (mejor que el shell, que tiene caracteristicas no deseables)

```yml
FROM ubuntu:trusty
COPY ["loop.sh", "/"]
CMD ["/loop.sh"]
```

## Contenedores ejecutables

Forma de ingresar parámetros de entrada

```yml
FROM ubuntu:trusty
ENTRYPOINT ["/bin/ping", "-c", "3"]
CMD ["localhost"]
```

Sino se ingresa parámetro de entrada, toma el valor por defecto 

```bash
docker run --name pinger ping
```

Con parámetros de entrada

```bash
docker run --name pinger ping google.com
```

## Dockerignore

Archivo .dockerignore ignora archivos y extensiones

## Multi-stage build

Consiste en el dockerfile, tener un build con los test y seguido de eso el build con los recursos necesarios para el ambiente, en este caso agregar los fuentes de la imagen de test + todas las dependencias cacheadas en la imagen de test 

## Docker in Docker

Se puede correr docker en docker, apundando a socket del contenedor y ambos dockers podran ver lo mismo, solo para Mac y Linux.

```bash 
docker run -it --rm -v /var/run/docker.sock:/var/run/docker.sock docker:latest 
```

