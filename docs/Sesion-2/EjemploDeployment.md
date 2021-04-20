# Ejemplo de deployment de una app en kubernetes:

<br>

Como sabemos, para trabajar con kubernetes necesitamos un cluster con dos nodos Worker y un nodo Master del que no disponemos.
Por eso, para practicar en nuestro ordenador, vamos a utilizar `Minikube`.

Minikube nos permite simular en nuestro equipo (solo necesitamos un ordenador) un cluster entero con su nodo Master y un nodo worker.

Podemos inicializarlo de la siguiente manera:

```
    $ minikube start
```

Esto hará que minikube empiece a funcionar, simulando asi nuestro entorno de prueba local.

<br>
<br>

Ahora lo que vamos a hacer es clonar el repositorio de la App que queremos levantar.
En este caso vamos a utilizar la 'Pokeapp', una Appweb de Pokemon desarrollada en Angular por Antonio Moruno (compañero del grado de informatica en la UCO y delegado en el Aula de Software Libre).

<br>

```
    $ git clone https://github.com/moruno21/pokeapp
```

Clonamos el repositorio a nuestro directorio de trabajo (el escritorio por ejemplo).

<br>

Ahora vamos a crear un Dockerfile que nos genere la imagen que necesitamos:

```
    $ cat Dockerfile

    ### STAGE 1

    FROM node:10-alpine as build-step

    RUN mkdir -p /app

    WORKDIR /app

    COPY package.json /app

    RUN npm install

    COPY ./ /app

    RUN npm run build --prod

    ### STAGE 2

    FROM nginx:1.17.1-alpine

    COPY --from=build-step /app/dist/pokeapi/ /usr/share/nginx/html
```

Con este Dockerfile podremos genera la imagen que usarán nuestros contenedores de la siguiente forma:

```
    $ docker build -t pokeapp-image .
```

Hemos generado nuestra imagen y podemos comprobarlo haciendo `$ docker images`

Ahora creamos nuestro `pokedeploy.yaml` y nuestro `pokeloadbalancer.yaml`.
