# Utilizando Docker para desarrollar aplicaciones

Ejecutar la imagen
* --rm elimina el contenedor al bajar la aplicación 

```bash
docker run --rm -p 3000:3000 platziapp
```

Corre el contenedor monitoreando cambios en los archivos de Dockerfile

```bash
docker run --rm -p 3000:3000 -v C:\Dev\Git\docker\index.js:/usr/src/index.js platziapp
```

## Crear una red

Crear una red, en que los contenedores podrán usarla cuando quieran

```bash
docker network create --attachable platzinet
```

Contenedor de mongo 

```bash
docker run -d --name db mongo
```

Conectar mongo con la red platzinet 

```bash
docker network connect platzinet db
```

Correr el contenedor de la app

```bash
docker run -d --name app -p 3000:3000 --env MONGO_URL=mongodb://db:27017/test platziapp
```

Conectar el contenedor app a la red platzinet

```bash
docker network connect platzinet app 
```