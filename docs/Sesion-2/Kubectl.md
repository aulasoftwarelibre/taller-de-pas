# Kubectl

![Kubectl](https://geekflare.com/wp-content/uploads/2021/03/kubectl.jpg)

A través de la herramienta de línea de comandos kubectl podemos controlar nuestors clústers de Kubernetes. 

La configuración de `kubectl` reside en el archivo `config` que se encuentra en el directorio `$HOME/.kube` Aunque si queremos, también podemos especificar otros archivos [kubeconfig](/docs/concepts/configuration/organize-cluster-access-kubeconfig/) configurando la variable de entorno KUBECONFIG o configurando la bandera [`--kubeconfig`](/docs/concepts/configuration/organize-cluster-access-kubeconfig/) flag..

## Sintaxis

Los comandos de Kubectl tienen el siguiente formato:

```shell
kubectl [command] [TYPE] [NAME] [flags]
```

Donde `command`, `TYPE`, `NAME`, y `flags` son:

* `command`: Operación que se desea realizar sobre uno o más recursos. Por ejemplo: `create`, `get`, `describe`, `delete`.

* `TYPE`: Indica el [tipo de recurso](#resource-types) al que se le aplica la operación. Los tipos de recursos son insensibles a las mayúsculas y se pueden indicar tanto en singular, plural o incluso de forma abreviada.
Por ejemplo los siguientes comandos producen la misma salida:

   ```shell
   kubectl get pod pod1
   kubectl get pods pod1
   kubectl get po pod1
   ```

* `NAME`: Hace referencia al nombre del recurso al que se le va a aplicar dicha operación. Los nombres son sensibles a las mayúsculas. Y si lo omitimos, se nos mostrará la información de todos los recursos disponibles. Por ejemplo: `kubectl get pods`.

Al realizar una operación en varios recursos, puede especificar cada recurso por tipo y nombre o especificar uno o más archivos:

   * Para especificar recursos por tipo y nombre:

      * Agrupar recursos si son del mismo tipo:  `TYPE1 name1 name2 name<#>`.<br/>
      Ejemplo: `kubectl get pod example-pod1 example-pod2`

      * Especificar distintos tipos de recursos individualmente:  `TYPE1/name1 TYPE1/name2 TYPE2/name3 TYPE<#>/name<#>`.<br/>
      Ejemplo: `kubectl get pod/example-pod1 replicationcontroller/example-rc1`

   * Especificar recursos con uno o más archivos:  `-f file1 -f file2 -f file<#>`

      * [Utilice YAML mejor que JSON](/docs/concepts/configuration/overview/#general-configuration-tips) ya que YAML suele ser más user-friendly, sobretodo para ficheros de configuración.<br/>
     Ejemplo: `kubectl get -f ./pod.yaml`

* `flags`: Permite especificar banderas. Por ejemplo, puede utilizar las banderas `-s` o `--server` para especificar la dirección y el puerto a la API de Kubernetes.<br/>

!!! Atención 
Las banderas que especifiquemos a través de la linea de comandos anula los valores predeterminados de las banderas y las variables de entorno correspondientes.
!!!

Si necesitas ayuda escribe `kubectl help` en la consola.

## Operaciones

La siguiente tabla incluye una breve descripión y la sintaxis general de las operaciones de `kubectl`:

Operation       | Syntax    |       Description
-------------------- | -------------------- | --------------------
`alpha`    | `kubectl alpha SUBCOMMAND [flags]` | List the available commands that correspond to alpha features, which are not enabled in Kubernetes clusters by default.
`annotate`    | <code>kubectl annotate (-f FILENAME &#124; TYPE NAME &#124; TYPE/NAME) KEY_1=VAL_1 ... KEY_N=VAL_N [--overwrite] [--all] [--resource-version=version] [flags]</code> | Add or update the annotations of one or more resources.
`api-resources`    | `kubectl api-resources [flags]` | List the API resources that are available.
`api-versions`    | `kubectl api-versions [flags]` | List the API versions that are available.
`apply`            | `kubectl apply -f FILENAME [flags]`| Apply a configuration change to a resource from a file or stdin.
`attach`        | `kubectl attach POD -c CONTAINER [-i] [-t] [flags]` | Attach to a running container either to view the output stream or interact with the container (stdin).
`auth`    | `kubectl auth [flags] [options]` | Inspect authorization.
`autoscale`    | <code>kubectl autoscale (-f FILENAME &#124; TYPE NAME &#124; TYPE/NAME) [--min=MINPODS] --max=MAXPODS [--cpu-percent=CPU] [flags]</code> | Automatically scale the set of pods that are managed by a replication controller.
`certificate`    | `kubectl certificate SUBCOMMAND [options]` | Modify certificate resources.
`cluster-info`    | `kubectl cluster-info [flags]` | Display endpoint information about the master and services in the cluster.
`completion`    | `kubectl completion SHELL [options]` | Output shell completion code for the specified shell (bash or zsh).
`config`        | `kubectl config SUBCOMMAND [flags]` | Modifies kubeconfig files. See the individual subcommands for details.
`convert`    | `kubectl convert -f FILENAME [options]` | Convert config files between different API versions. Both YAML and JSON formats are accepted.
`cordon`    | `kubectl cordon NODE [options]` | Mark node as unschedulable.
`cp`    | `kubectl cp <file-spec-src> <file-spec-dest> [options]` | Copy files and directories to and from containers.
`create`        | `kubectl create -f FILENAME [flags]` | Create one or more resources from a file or stdin.
`delete`        | <code>kubectl delete (-f FILENAME &#124; TYPE [NAME &#124; /NAME &#124; -l label &#124; --all]) [flags]</code> | Delete resources either from a file, stdin, or specifying label selectors, names, resource selectors, or resources.
`describe`    | <code>kubectl describe (-f FILENAME &#124; TYPE [NAME_PREFIX &#124; /NAME &#124; -l label]) [flags]</code> | Display the detailed state of one or more resources.
`diff`        | `kubectl diff -f FILENAME [flags]`| Diff file or stdin against live configuration.
`drain`    | `kubectl drain NODE [options]` | Drain node in preparation for maintenance.
`edit`        | <code>kubectl edit (-f FILENAME &#124; TYPE NAME &#124; TYPE/NAME) [flags]</code> | Edit and update the definition of one or more resources on the server by using the default editor.
`exec`        | `kubectl exec POD [-c CONTAINER] [-i] [-t] [flags] [-- COMMAND [args...]]` | Execute a command against a container in a pod.
`explain`    | `kubectl explain  [--recursive=false] [flags]` | Get documentation of various resources. For instance pods, nodes, services, etc.
`expose`        | <code>kubectl expose (-f FILENAME &#124; TYPE NAME &#124; TYPE/NAME) [--port=port] [--protocol=TCP&#124;UDP] [--target-port=number-or-name] [--name=name] [--external-ip=external-ip-of-service] [--type=type] [flags]</code> | Expose a replication controller, service, or pod as a new Kubernetes service.
`get`        | <code>kubectl get (-f FILENAME &#124; TYPE [NAME &#124; /NAME &#124; -l label]) [--watch] [--sort-by=FIELD] [[-o &#124; --output]=OUTPUT_FORMAT] [flags]</code> | List one or more resources.
`kustomize`    | `kubectl kustomize <dir> [flags] [options]` | List a set of API resources generated from instructions in a kustomization.yaml file. The argument must be the path to the directory containing the file, or a git repository URL with a path suffix specifying same with respect to the repository root.
`label`        | <code>kubectl label (-f FILENAME &#124; TYPE NAME &#124; TYPE/NAME) KEY_1=VAL_1 ... KEY_N=VAL_N [--overwrite] [--all] [--resource-version=version] [flags]</code> | Add or update the labels of one or more resources.
`logs`        | `kubectl logs POD [-c CONTAINER] [--follow] [flags]` | Print the logs for a container in a pod.
`options`    | `kubectl options` | List of global command-line options, which apply to all commands.
`patch`        | <code>kubectl patch (-f FILENAME &#124; TYPE NAME &#124; TYPE/NAME) --patch PATCH [flags]</code> | Update one or more fields of a resource by using the strategic merge patch process.
`plugin`    | `kubectl plugin [flags] [options]` | Provides utilities for interacting with plugins.
`port-forward`    | `kubectl port-forward POD [LOCAL_PORT:]REMOTE_PORT [...[LOCAL_PORT_N:]REMOTE_PORT_N] [flags]` | Forward one or more local ports to a pod.
`proxy`        | `kubectl proxy [--port=PORT] [--www=static-dir] [--www-prefix=prefix] [--api-prefix=prefix] [flags]` | Run a proxy to the Kubernetes API server.
`replace`        | `kubectl replace -f FILENAME` | Replace a resource from a file or stdin.
`rollout`    | `kubectl rollout SUBCOMMAND [options]` | Manage the rollout of a resource. Valid resource types include: deployments, daemonsets and statefulsets.
`run`        | <code>kubectl run NAME --image=image [--env="key=value"] [--port=port] [--dry-run=server&#124;client&#124;none] [--overrides=inline-json] [flags]</code> | Run a specified image on the cluster.
`scale`        | <code>kubectl scale (-f FILENAME &#124; TYPE NAME &#124; TYPE/NAME) --replicas=COUNT [--resource-version=version] [--current-replicas=count] [flags]</code> | Update the size of the specified replication controller.
`set`    | `kubectl set SUBCOMMAND [options]` | Configure application resources.
`taint`    | `kubectl taint NODE NAME KEY_1=VAL_1:TAINT_EFFECT_1 ... KEY_N=VAL_N:TAINT_EFFECT_N [options]` | Update the taints on one or more nodes.
`top`    | `kubectl top [flags] [options]` | Display Resource (CPU/Memory/Storage) usage.
`uncordon`    | `kubectl uncordon NODE [options]` | Mark node as schedulable.
`version`        | `kubectl version [--client] [flags]` | Display the Kubernetes version running on the client and server.
`wait`    | <code>kubectl wait ([-f FILENAME] &#124; resource.group/resource.name &#124; resource.group [(-l label &#124; --all)]) [--for=delete&#124;--for condition=available] [options]</code> | Experimental: Wait for a specific condition on one or many resources.

Para más información visite la documentación de [kubectl](/docs/reference/kubectl/kubectl)