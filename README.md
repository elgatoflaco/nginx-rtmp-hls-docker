# nginx-rtmp-hls

[**Docker**](https://www.docker.com/) image con [**Nginx**](http://nginx.org/en/) usando el módulo [**nginx-rtmp-module**](https://github.com/arut/nginx-rtmp-module), transmitir videos en directo.

## Descripción

Esta imagen de [**Docker**](https://www.docker.com/) puede ser usada para crear un servidor multimeda RTMP / HLS para transmitir videos en directo usando [**Nginx**](http://nginx.org/en/) y el módulo [**nginx-rtmp-module**](https://github.com/arut/nginx-rtmp-module).


## Uso

* El uso es simple, con estos dos comandos:

Primero crearemos una imagen con el fichero Dockerfile, con la etiqueta `nginx-rmtp-hls:1.0` esto nos ayudará a encontrarla luego más fácil.

```bash
docker build --tag nginx-rmtp-hls:1.0 .
```

Ahora ejecutaremos la imagen que hemos creado en un contenedor.

```bash
docker run -d -p 1935:1935 -p 8080:8080 --name nginx-rtmp nginx-rmtp-hls:1.0
```


## Cómo probar con OBS Studio y VLC

* Run a container with the command above


* Abrir [OBS Studio](https://obsproject.com/)
* Haz clic en el botón de "Ajutstes"
* ve a la sección "Emisión"
* En "Servicio" selecciona "Personalizado..."
* En el "Servidor" introduce `rtmp://<ip_del_host>/live` reemplazando `<ip_del_host>` con la ip que tengas corriendo el contenedor Docker. Por ejemplo: `rtmp://192.168.1.110/live`
* En la "Clave de retransmisión" podemos poner cualquierda, por ejemplo `test` quedando la url `rtmp://<ip_del_host>/live/test`.
* Hacemos click en "Aceptar"
* En la sección "Fuentes" pulsamos "Añadir" que es el botón (`+`) y seleccionados la entrada que quedamos.
* Por último pulsamos "Iniciar Tránsmisión"


* Abre [VLC](http://www.videolan.org/vlc/index.html)
* Click en "Archivo"
* Abrir "Red"
* Introducir en "URL" la siguiente dirección `rtmp://<ip_del_host>/live/<key>` reemplazando `<ip_del_host>` por la dirección ip donde está corriendo el contenedor Docker y `<key>` por la clave que tengamos en OBS. FPor ejemplo: `rtmp://192.168.1.110/live/test`
* Click en "Play"