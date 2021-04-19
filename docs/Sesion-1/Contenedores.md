# Contenedores

Los contenedores son instancias de las imágenes que hemos creado o hemos descargado y que se ejecutan de forma aislada.

## Listado

Para ver el listado de contenedores, usaremos:

    - docker container ls

    o

    - docker ps (versión abreviada)

Si lo ejecutamos, nos dará un listado vacío porque no hay ningún contenedor activo.

para ver el listado de contenedores parados, usaremos:

    - docker container ls -a

    o

    - docker ps -a (versión abreviada)

## Ejecutar comandos dentro de una contenedor

Ya hemos usado el comando **_docker run_** para crear e iniciar nuestro contenedro, pero también podemos usar este comando para ejecutar programas que estén dentro del contenedor:

    docker run --name ubuntu_bash --rm -i -t ubuntu bash

Pero esra forma de ejecutar las cosas, crea un nuevo contenedor. Si queremos ejecutar un comando en un contenedor que ya esté iniciado, usaremos:

    docker container exec

Sin cerrar este terminal, ejecutamos en otra terminal:

    docker exec -w /tmp ubuntu_bash touch my_file.sh

Donde:

1. -w -> indica el directorio de trabajo

2. ubuntu_bash -> indicamos el contenedor donde queremos ejecutar el comando

3. touch my_file.sh -> el comando a ejecutar

Para cerrar y borrar el contenedor, usamos:

    Control+c

## Iniciar un contenedor

Para inciar un contenedor parado, usaremos:

    docker container start

## Detener un contenedor

Para detener un contenedor iniciado, usaremos:

    docker container stop (id / nombre)

Indicando su id o su nombre

## Borrar un contenedor

Un contenedor parada ocupa espacio. Si hemos dejado de necesitar uin contenedor, podemos usar el siguiente comando para borrarlo:

    docker container rm (id / nombre)

Indicando al igual que con la opción de detener, su id o nombre.
