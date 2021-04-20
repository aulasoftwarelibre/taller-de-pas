# Instalación

Existen dos versiones de Dcoker, una libre y otra que no lo es. Nos ouparemos exclusivamente de la primera: Docker CE (Community Edition)

### Disponibilidad

Docker CE está disponible para los siguientes sistemas GNU/Linux: CentOS, Debian, Fedora , Raspbian y Ubuntu. Y esta soportado por aruitecturas como x86_64 / amd64 , ARM y ARM64 / AARCH64.

### Instalación

Debido a que, dependiendo de la distribución, la forma de instalarlo difiere, es mejor consultar la documentación oficial para saber como instalar Docker en tu máquina.

- Ubuntu: [https://docs.docker.com/engine/install/ubuntu/](https://docs.docker.com/engine/install/ubuntu/)
- Debian: [https://docs.docker.com/engine/install/debian/](https://docs.docker.com/engine/install/debian/)
- CentOS: [https://docs.docker.com/engine/install/centos/](https://docs.docker.com/engine/install/centos/)
- Fedora: [https://docs.docker.com/engine/install/fedora/](https://docs.docker.com/engine/install/fedora/)

Para saber si tienes Docker bien instalado, los tutoriales oficiales siempre te indican que inicies un contenedor de ejemplo. Esto es lo que sucede:

    $ sudo docker run hello-world
    Unable to find image 'hello-world:latest' locally
    latest: Pulling from library/hello-world
    d1725b59e92d: Pull complete
    Digest: sha256:0add3ace90ecb4adbf7777e9aacf18357296e799f81cabc9fde470971e499788
    Status: Downloaded newer image for hello-world:latest

    Hello from Docker!
    This message shows that your installation appears to be working correctly.

    To generate this message, Docker took the following steps:
     1. The Docker client contacted the Docker daemon.
     2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
     3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
     4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

    To try something more ambitious, you can run an Ubuntu container with:
    $ docker run -it ubuntu bash

    Share images, automate workflows, and more with a free Docker ID:
    https://hub.docker.com/

    For more examples and ideas, visit:
    https://docs.docker.com/get-started/
    ```

En la línea 1 estamos ejecutando el cliente de Docker, y estamos indicando que queremos ejecutar un contenedor a partir de la imagen [hello-world](https://hub.docker.com/_/hello-world/) del registro público de Docker.

Si es la primera vez que hemos ejecutado esa imagen, nos aparecerá la línea 2, que indica que la imagen no puede ser encontrada y va a proceder a buscarla, por defecto, en el registro público. Si tenemos conexión a Internet se descargará la imagen (línea 6) y automáticamente creará un contenedor.

Tanto si se ha descargado la imagen o ya estaba descargada, el contenedor se ejecutará, obteniendo el texto de bienvenida que se ve en el cuadro anterior.

### Configuración del usuario

Si estamos usando _Docker_ en nuestro ordenador, podemos configurar nuestro usuario para usar el cliente sin tener que poner sudo delante. Para ello, debemos de ejecutar el siguiente comando:

    sudo usermod -aG docker $USER

Para que surjan efecto los cambios, debemos de cerrar y volver a abrir la sesión.

### Herramientas

También es necesario tener una herramienta llamada Docker Compose. Puedes instalarla siguiendo las instrucciones que se encuentra en la página de [Instalación de Docker Compose](https://docs.docker.com/compose/install/) .

Sin embargo, si usas Ubuntu o Debian, podemos instalarlo con el siguiente comando:

    sudo apt install docker-compose
