# Imágenes

Son la bade de _Docker_ ya que nuestros contenedores se iniciarán a partir de ellas. Como ya se indicó en la introducción, es una plantilla de solo lectura, que se crea incorporando los requisitos necesarios para cumplir el objetivo para el cual fue creada.

## Buscar imágenes

Crear una imagen desde cero supone un esfuerzo grandísimo, así que lo normal es partir o usar una ya creada.

Para ello buscaremos en los registros que son el lugar donde se almacenan. Hay un registro oficial [https://hub.docker.com](https://hub.docker.com), pero nada impide a otras organizaciones, o incluso a nosotros mismo, tener un registro propio. Estos pueden ser tanto públicos como privados.

Vamos a imaginarnos que queremos crear una web con _Wordpress_. Si buscamos en el registro, encontraremos una imagen llamada _wordpress_, con la etiqueta oficial. La recomendación es que siempre busquemos imágenes oficiales, ya que están mantenidas y bien documentadas.

## Gestión de imágenes

### Descarga

Las imagenes que nos descargamos, se identifican tanto por nombre como por versión. De esa manera, podemos tener distintas versiones de una misma imagen. En la página del registro veremos una pestaña con el nombre _Tags_, con las versiones disponibles.

Para usar una en concreto, se usa dos puntos seguido del nombre de la versión. SI no se indica nada, como hasta ahora, por defecto se descarga la etiquetata como _latest_

Para descargar imágenes, usaremos:

    docker pull

### Listado

Para ver el listado de imagenes disponibles, usaremos:

    docker images

### Borrado

Si queremos dejar de usar alguna imagen, usaremos:

    docker rmi
