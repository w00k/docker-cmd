# Ejecutar archivo 

Para correr el archivo es necesario usar: 

```bash
docker build -t ubuntu:platzi .
```

* -t es el tag que le vamos a dar
* . directorio actual como contexto de build 

Toda imagen es un conjunto de capas o layers

# Publicar una imagen

Primero es encesario loguearse 

```bash
docker login
```

Cambiar *tag* de la imagen 

```bash
docker tag ubuntu:platzi w00kyx/ubuntu:platzi
```

* tag cambia el tag que existe de la imagen 
* w00kyx corresponde al repositorio del usuario en DockerHub
* ubuntu:platzi corresponde a imagen tag

# Publicar la imagen

Primero se genera el nuevo tag, para la cuenta a la que se quiere hacer push

```bash
docker build -t ubuntu:platzi .
```
* -t tag que se asignará a mi cuenta
* . usar esta carpera como build context

```bash
 docker push w00kyx/ubuntu:platzi
 ```

