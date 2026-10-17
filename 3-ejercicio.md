## Esquema para el ejercicio
![Imagen](esquema-ejercicio3.PNG)

### Crear red net-wp

```
docker network create net-wp
```

### Para que persista la información es necesario conocer en dónde mysql almacena la información.

En el esquema del ejercicio carpeta del contenedor (a) es /var/lib/mysql

Ruta carpeta host: .../ejercicio3/db

### ¿Qué contiene la carpeta db del host?

Nada, la carpeta recíen se ha creado y no contiene ningún archivo.

### Crear un contenedor con la imagen mysql:8  en la red net-wp, configurar las variables de entorno: MYSQL_ROOT_PASSWORD, MYSQL_DATABASE, MYSQL_USER y MYSQL_PASSWORD

```
docker run -d --name contenedormysql --network net-wp -v ~/ejercicio3/db:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=password -e MYSQL_DATABASE=db -e MYSQL_USER=usuario -e MYSQL_PASSWORD=1234 mysql:8
```

### ¿Qué observa en la carpeta db que se encontraba inicialmente vacía?

Ahora contiene carpetas como #innodb_redo/, #innodb_temp, mysql/, performance_schema/, sys/ y algunos archivos que se crean y se eliminan.

### Para que persista la información es necesario conocer en dónde wordpress almacena la información.

En el esquema del ejercicio la carpeta del contenedor (b) es /var/www/html

Ruta carpeta host: .../ejercicio3/www

### Crear un contenedor con la imagen wordpress en la red net-wp, configurar las variables de entorno WORDPRESS_DB_HOST, WORDPRESS_DB_USER, WORDPRESS_DB_PASSWORD y WORDPRESS_DB_NAME (los valores de estas variables corresponden a los del contenedor creado previamente)

```
docker run -d --name contenedorwordpress --network net-wp -p 9500:80 -v ~/ejercicio3/www:/var/www/html -e WORDPRESS_DB_HOST=contenedormysql -e WORDPRESS_DB_USER=usuario -e WORDPRESS_DB_PASSWORD=1234 -e WORDPRESS_DB_NAME=db wordpress
```

### Personalizar la apariencia de wordpress y agregar una entrada

### Eliminar el contenedor y crearlo nuevamente, ¿qué ha sucedido?

Se visualiza la entrada agregada y la apariencia de wordpress se ha mantenido porque esta información se almacenó y persistió en el volumen.

