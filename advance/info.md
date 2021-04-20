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