# ¿Como funciona?

![Kubernetes Logo](https://unpocodejava.files.wordpress.com/2020/01/image006.jpg)

Kubernetes define un conjunto de bloques de construcción que conjuntamente proveen los mecanismos para el despliegue, mantenimiento y escalado de aplicaciones. Los componentes que forman Kubernetes están diseñados para estar débilmente acoplados pero a la vez ser extensibles para que puedan soportar una gran variedad de flujos de trabajo. La extensibilidad es provista en gran parte por la API de Kubernetes, que es utilizada por componentes internos así como extensiones y contenedores ejecutados sobre Kubernetes.

## Componentes:

### Pods

La unidad básica de planificación en Kubernetes se denomina pod. Esta agrega un nivel de abstracción más elevado a los componentes en contenedores. Un pod consta de uno o más contenedores en los que se garantiza su ubicación en el mismo equipo anfitrión y pueden compartir recursos. 

Cada pod en Kubernetes es asignado a una única dirección IP (dentro del clúster) que permite a las aplicaciones utilizar puertos sin riesgos de conflictos. Un pod puede definir un volumen, como puede ser un directorio de disco local o un disco de red, y exponerlo a los contenedores dentro del pod. Los pods pueden ser administrados manualmente a través de la API de Kubernetes, o su administración puede ser delegada a un controlador.

### Nodo

El nodo, también conocido como esclavo o worker, es la máquina física (o virtual) donde los contenedores (flujos de trabajos) son desplegados. Cada nodo en el clúster debe ejecutar la rutina de tiempo de ejecución (como Docker), así como también los componentes mencionados más abajo, para comunicarse con el maestro para la configuración en red de estos contenedores.

### Etiquetas y selectores

Kubernetes permite a los clientes (usuarios o componentes internos) vincular pares clave-valor llamados etiquetas (en inglés label) a cualquier objeto API en el sistema, como pods o nodos. Correspondientemente, selectores de etiquetas son consultas contra las etiquetas que resuelven a los objetos que las satisfacen​.

Las etiquetas y los selectores son el mecanismo principal de agrupamiento en Kubernetes, y son utilizados para determinar los componentes sobre los cuales aplica una operación.

Por ejemplo, si un pod de una aplicación tiene la etiqueta para un nivel del sistema (“front-end”, “back-end”, por ejemplo) y un release_track (“canary”, “production”, por ejemplo), entonces una operación sobre todos los nodos “back-end” y “canary” podría utilizar un selector de etiquetas como el siguiente:

      nivel=back-end AND release_track=canary