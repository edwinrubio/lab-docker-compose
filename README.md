# Laboratorio de Docker Compose

## Problema

Dentro de la empresa Pollito, se tenía una implementación con docker-compose que los desarrolladores usaban para hacer pruebas, pero por un incidente de seguridad, esta implementación se vio corrompida. El objetivo del taller es habilitar nuevamente el uso del docker-compose con todos sus componentes y asi los desarrolladores los puedan usar de nuevo.

## Compilar y Publicar

- Crear un usuario en Docker Hub.
- Compilar los Dockerfiles en los siguientes directorios y publicar en Docker Hub:
  - `./configuration/php`
  - `./configuration/python`

## Contexto del Entorno

La implementación tiene un docker-compose que pone en funcionamiento 4 contenedores:

- php
- nginx
- mysql
- python

## Especificaciones

### PHP

- Debe tener dos volúmenes de la siguiente manera:
  - **HOST ->** `./volumes/nginx/:/var/www/html` **CONTAINER**
  - **HOST ->** `./configuration/php/www.conf:/usr/local/etc/php-fpm.d/www.conf` **CONTAINER**
- Debe tener el puerto 9200 abierto y establecer las siguientes variables de entorno: `MYSQL_USER`, `MYSQL_PASSWORD`.
- Compilar la imagen desde esta ubicación: `./configuration/php, subirla a la dockerhub y usarla dentro del docker-compose.yaml

### NGINX

- Debe tener los siguientes volúmenes en su configuración:
  - **HOST ->** `./volumes/nginx/:/var/www/html` **CONTAINER**
  - **HOST ->** `./volumes/logs:/var/log/nginx` **CONTAINER**
  - **HOST ->** `./configuration/nginx/default.conf:/etc/nginx/conf.d/default.conf` **CONTAINER**
- Agregar un archivo llamado `index.html` con tu nombre dentro de `/var/www/html`.

### PYTHON

- Compilar la imagen desde esta ubicación: `./configuration/python`.
- generar la imagen, ponerla dentro de la dockerhub y usarla en docker-compose.yaml
- El servicio del contenedor debe estar expuesto en el puerto 5000.

### Archivo de Variables

- Crear un archivo para leer variables y usarlas en el proyecto para usar credenciales y datos sencibles.

### Red

- Todos los contenedores deben estar conectados a la misma red.
## Test de la correcta instalación de PHP

Antes de comenzar a trabajar con el entorno hay que probar su funcionamiento.
Accediendo a http://localhost:88/test/phpinfo.php se comprueba si funciona correctamente el contenedor de php. Si no es así se mostrará una pantalla de error.



## Uso de phpMyAdmin con docker

PhpMyadmin es un cliente web para gestionar bases de datos de manera sencilla. Por comodidad vamos a utilizar una imagen docker del propio creador PhpMyAdmin. Una vez que se ha levantado el entorno de Nginx y Mysql para correr phpMyadmin por el puerto **8081** se debe lanzar el comando:

```
docker run --network={network} --name phpmyadmin -d -e PMA_HOST=mysql --link mysql:db -p 8081:80 phpmyadmin/phpmyadmin
```

Se puede acceder a la aplicación desde la url: **http://localhost:8081**

