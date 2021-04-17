# Docker Compose

Levantar docker-compose

```bash
docker-compose up
```

Levantar docker-compose en modo background

```bash
docker-compose up -d
```

Detener docker-compose 

```bash
docker-compose stop
```

Ver el log de un contenedor

```bash
docker-compose logs app
```

Ingresar al contenedor 

```bash
docker-compose exec app bash
```

Baja y destrulle el/los contenedor/es

```bash
docker-compose down
```

## Build de código

Nuestro yml debe quedar con el tag **build** y **el path del source** 

```yml
version: "3.8"

services:
  app:
    build: .
    environment:
      MONGO_URL: "mongodb://db:27017/test"
    depends_on:
      - db
    ports:
      - "3000:3000"

  db:
    image: mongo
```

Luego es necesario hacer el build de los fuentes

```bash
docker-compose build
```

Finalmente, es necesario levantar el compose. 

```bash
docker-compose up -d 
```

* Nota : De esta forma, se debe hacer un build cada vez que el código cambia. 

### Una solución manual

Cada vez que hay un cambio en los fuentes, hacer que *docker-compose* genere la imagen del app 

```bash
docker-compose build app 
```

A continuación, correr el docker-compose para que detecte el cambio en la imagen y la haga ejecute

```bash
docker-compose up -d 
```

### Solución en Mac y Linux 

Agregar los tags: 
* **volumes** : con la . a compartir y la carpeta node_modules a no modificar en la imagen
* **comand** : usando el npx para monitorear el archivo e identifique los cambios de los fuentes

```yml
version: "3.8"

services:
  app:
    build: .
    environment:
      MONGO_URL: "mongodb://db:27017/test"
    depends_on:
      - db
    ports:
      - "3000:3000"
    volumes: 
      - .:/usr/src
      - /usr/src/node_modules
    command: npx nodemon index.js

  db:
    image: mongo
```

Ejecutar el compose 

```bash
docker-compose up -d  
```