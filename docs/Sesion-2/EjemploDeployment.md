# Ejemplo de deployment

![PokeApp](https://pokeapp-git-master-moruno21.vercel.app/assets/developedBy.png)

Como sabemos, para trabajar con kubernetes necesitamos un cluster con dos nodos Worker y un nodo Master del que no disponemos.
Por eso, para practicar en nuestro ordenador, vamos a utilizar `Minikube`.

Minikube nos permite simular en nuestro equipo un cluster entero con su nodo Master y un nodo worker.

Podemos inicializarlo de la siguiente manera:

     minikube start

Esto hará que minikube empiece a funcionar, simulando asi nuestro entorno de prueba local.

Ahora lo que vamos a hacer es clonar el repositorio de la App que queremos levantar.
En este caso vamos a utilizar la 'Pokeapp', una Appweb de Pokemon desarrollada en Angular por Antonio Moruno (compañero del grado de informatica en la UCO y delegado en el Aula de Software Libre).

    git clone https://github.com/moruno21/pokeapp 

Clonamos el repositorio a nuestro directorio de trabajo (el escritorio por ejemplo).

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

    docker build -t pokeapp-image .

Hemos generado nuestra imagen y podemos comprobarlo haciendo `$ docker images`

Ahora creamos nuestro `pokedeploy.yaml` y nuestro `pokeloadbalancer.yaml`.

```
    $ cat pokedeployment.yaml

    apiVersion: apps/v1
    kind: Deployment
    metadata:
      creationTimestamp: null
      labels:
          app: pokeapp
          name: pokeapp
    spec:
      replicas: 5
      selector:
        matchLabels:
          app: pokeapp
      strategy: {}
      template:
        metadata:
          creationTimestamp: null
          labels:
            app: pokeapp
        spec:
          containers:
          - name: pokeapp
            image: docker.io/jdes01/pokeimage
            imagePullPolicy: IfNotPresent
            resources: {}
            ports:
              - containerPort: 80
    status: {}
```

Con esto creamos un deployment en el que levantaremos 5 replicas (5 pods) que se comunicaran a traves del puerto 80 y que contendran uno de nuestros contenedores (cuya imagen creamos con el Dockerfile).

Ahora hacemos el `pokeloadbalancer.yaml`:

```
    $ cat pokeloadbalancer.yaml

    apiVersion: v1
    kind: Service
    metadata:
      name: pokeapp-loadbalancer
      labels:
        run: pokeapp
    spec:
      type: LoadBalancer
      ports:
        - name: "80"
          port: 80
          targetPort: 80
          protocol: TCP
      selector:
        app: pokeapp
```

Este será nuestro principal servicio. Redistribuirá el tráfico que sostenga nuestra aplicacion, "balanceando la carga" de los pods para no saturarlos.

Ahora que hemos desplegado nuestros pods, cuyo estado comprobamos con 

    kubectl get pods 

Y nuestro servicio, que podemos ver con 

    kubectl get services

Podemos decir que ya hemos conpletado el deploy de nuestra app. De igual forma, podemos ver informacion del mismo con:

    kubectl get deployments

Al tratarse de un ejemplo ejecutado en un cluster de prueba, expondremos nuestro cluster usando 

    minikube tunnel

Ahora, si volvemos a ejecutar `kubectl get services` veremos que a nuestro pokeLoadBalancer se le ha asignado una IP externa.

Podemos escribirla en nuestro navegador y comprobar que esta desplegada.
Con un servicio de DNS y un dominio podriamos hacer que cualquier persona la buscase.