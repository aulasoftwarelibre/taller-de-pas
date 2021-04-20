# Conceptos básicos

Vamos a ver varios conceptos que debemos conocer:

- Cluster: Conjunto de maquinas (ordenadores físicos, servidores, etc.) y todo su contenido. Por así decirlo, podemos definirlo como un 'todo'.

- Nodos: Cada máquina de nuestro cluster. Cada ordenador/servidor que use nuestro cluster será un nodo. En nuestro Cluster existirá un nodo Master y n nodos Worker.

- Pod: Unidad mínima de nuestro sistema. Cada nodo tendra de 1 a n pods, y cada uno puede tener dentro contenedores, volumenes o ambos.

- Servicios: Abstraccion que define los Pods que funcionan en los nodos de nuestro cluester y como se accede a estos.

<br>

Ahora que ya conocemos que objetos existen en un cluster de Kubernetes, vamos a definirlos en profundidad.

## Cluster

Como hemos dicho antes, nuestro cluster a partir de ahora va a ser nuestro 'todo'. Este estará compuesto por nuestros nodos Worker y el nodo Maser

!!! tip

    El tamaño minimo de nuestro cluster debe ser de un nodo Master y dos Worker.

![Cluster](images/cluster.png)
