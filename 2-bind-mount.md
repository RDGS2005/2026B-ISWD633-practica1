# BIND MOUNT
En un bind mount mapeamos (montar) un directorio o archivo específico del sistema de archivos del host con una parte del sistema de ficheros del contenedor.

```
docker run -d --name <nombre contenedor> -v <ruta carpeta host>:<ruta carpeta contenedor> <imagen> 
```
ó
```
docker run -d --name <nombre contenedor> --mount type=bind,source=<ruta carpeta host>,target=<ruta carpeta contenedor> <imagen>
```
- destination, dst, target: La ruta donde se monta el archivo o directorio en el contenedor.
- source, src: El origen del montaje.
  
### En tu computador crear una carpeta llamada nginx y dentro de esta carpeta crea otra llamada html. Como se aprecia en la figura.
![Volúmenes](directorio.PNG)

### Crear un contenedor con la imagen nginx:alpine, mapear todos por puertos, para la ruta carpeta host colocar el directorio en donde se encuentra la carpeta html en tu computador y para la ruta carpeta contenedor: /usr/share/nginx/html (esta ruta se obtiene al revisar la documentación de la imagen)
![Volúmenes](volumen-host.PNG)

```
docker run -d --name nginx -P -v ~/nginx/html:/usr/share/nginx/html nginx:alpine
```

### ¿Qué sucede al ingresar al servidor de nginx?

Se obtiene el código de estado 403 forbidden.

### ¿Qué pasa con el archivo index.html del contenedor?

No se encuentra el archivo index.html porque la carpeta del host ~/nginx/html se montó en /usr/share/nginx/html y está vacía.

### Ir a https://html5up.net/ y descargar un template gratuito, descomprirlo dentro de tu computador en la carpeta html
### ¿Qué sucede al ingresar al servidor de nginx?

En el navegador se puede ver la página del template gratuito (ya hay index.html) y ya no se obtiene el código de estado 403 forbidden.

### Eliminar el contenedor

```
docker rm -f nginx
```

### ¿Qué sucede al crear nuevamente un contenedor montado al directorio definidos anteriormente?

Se persisten los archivos del template gratuito y al acceder al servidor del nuevo contenedor se puede seguir viendo la página web.


