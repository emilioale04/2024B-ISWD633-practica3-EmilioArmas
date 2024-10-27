## Esquema para el ejercicio
![Imagen](img/esquema-ejercicio3.PNG)

### Crear red net-wp
```
docker network create net-wp
```

### Para que persista la información es necesario conocer en dónde mysql almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/
En el esquema del ejercicio carpeta del contenedor (a) es `/var/lib/mysql`

Ruta carpeta host: .../ejercicio3/db

### ¿Qué contiene la carpeta db del host?
Inicialmente se encuentra vacía.

### Crear un contenedor con la imagen mysql:8  en la red net-wp, configurar las variables de entorno: MYSQL_ROOT_PASSWORD, MYSQL_DATABASE, MYSQL_USER y MYSQL_PASSWORD
```
docker run -d --name mysql-cont --network net-wp -e MYSQL_ROOT_PASSWORD=password -e MYSQL_DATABASE=wordpressdb -e MYSQL_USER=admin -e MYSQL_PASSWORD=admin -v ${PWD}/ejercicio3/db:/var/lib/mysql mysql:8
```

### ¿Qué observa en la carpeta db que se encontraba inicialmente vacía?
Se encuentran los archivos del directorio de datos de mysql, entre ellos, los archivos de las bases de datos creadas.

### Para que persista la información es necesario conocer en dónde wordpress almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/
En el esquema del ejercicio la carpeta del contenedor (b) es `/var/www/html`

Ruta carpeta host: .../ejercicio3/www

### Crear un contenedor con la imagen wordpress en la red net-wp, configurar las variables de entorno WORDPRESS_DB_HOST, WORDPRESS_DB_USER, WORDPRESS_DB_PASSWORD y WORDPRESS_DB_NAME (los valores de estas variables corresponden a los del contenedor creado previamente)
```
docker run -d --name wordpress-cont --network net-wp -e WORDPRESS_DB_HOST=mysql-cont:3306 -e WORDPRESS_DB_USER=admin -e WORDPRESS_DB_PASSWORD=admin -e WORDPRESS_DB_NAME=wordpressdb -p 9500:80 -v ${PWD}/ejercicio3/www:/var/www/html wordpress:latest
```

### Personalizar la apariencia de wordpress y agregar una entrada

### Eliminar el contenedor y crearlo nuevamente, ¿qué ha sucedido?
Las configuraciones se mantuvieron y la entrada previamente creada se puede ver sin problema.

![alt text](screenshots/image-1.png)