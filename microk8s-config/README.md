# microk8s-config

## Información del equipo de computo utilizado

La información descrita a continuación relaciona solo la configuración usada para trabajar, no se habla de requisitos minimos ni de uso concreto o rendimiento total quedando fuera del alcance del proyecto esto debido a que se usara kubernetes pudiendo organizar, ejecutar el proyecto en otros entornos de kubernetes o usando servicios de Cloud.

- Sistema operarivo: Ubuntu 22.04.3
- Tipo de SO: 60 bits
- Memoria: 16,0 GiB
- Procesador: Intel® Core™ i3-10105F CPU @ 3.7GHz x 8
- Gráficos: NVIDIA Corporation GK208B [GeForce GT 710]
- almacenamiento: 1TB

## Instalación

```bash
$ sudo snap install microk8s --clasic
Se ha instalado microk8s (1.27/stable) v1.27.6 por canonical ✓
```

## Unirce al grupo

MicroK8s crea un grupo para permitir el uso fluido de comandos que requieren privilegios de administrador. Para agregar su usuario actual al grupo y obtener acceso al directorio de almacenamiento en caché .kube, ejecute los dos comandos siguientes:

```bash
$ sudo usermod -a -G microk8s $USER
$ sudo chown -f -R $USER ~/.kube
```

También deberás volver a ingresar a la sesión para que se realice la actualización del grupo, recomendación: cerrar y abrir una nueva terminal.

## Comprobar el estado

MicroK8s tiene un comando incorporado para mostrar su estado. Durante la instalación, puede utilizar el indicador ```--wait-ready``` para esperar a que se inicialicen los servicios de Kubernetes:

```bash
$ microk8s status --wait-ready
```

## Acceder a Kubernetes

MicroK8s incluye su propia versión de kubectl para acceder a Kubernetes (microk8s kubectl). El cual se usa para ejecutar comandos, monitorear y controlar su Kubernetes. 
En este momento creamos un alias en el archivo ```~/.bashrc``` guardamos el archivo, cerramos y abrimos una nueva terminal:

```text
## ~/.bashrc
...
alias kubectl="microk8s kubectl"
```

Por ejemplo, para ver su nodo:
```bash
$ kubectl get nodes
```

Para ver los servicios:
```bash
$ kubectl get services
```

## Usar complementos

MicroK8s utiliza el mínimo de componentes para un Kubernetes puro y liviano. Sin embargo, hay muchas funciones adicionales disponibles con solo presionar unas pocas teclas usando "complementos": componentes preempaquetados que brindarán capacidades adicionales para su Kubernetes, desde la simple administración de DNS hasta el aprendizaje automático con Kubeflow.

Para empezar se recomienda agregar gestión de DNS para facilitar la comunicación entre servicios. Para aplicaciones que necesitan almacenamiento, el complemento 'hostpath-storage' proporciona espacio de directorio en el host. Estos son fáciles de configurar:

```bash
$ microk8s enable dns
$ microk8s enable hostpath-storage
```

``` bash
deployment.apps/hostpath-provisioner created
storageclass.storage.k8s.io/microk8s-hostpath created
serviceaccount/microk8s-hostpath created
clusterrole.rbac.authorization.k8s.io/microk8s-hostpath created
clusterrolebinding.rbac.authorization.k8s.io/microk8s-hostpath created
Storage will be available soon.
```

## Habilitar el complemento de Ingress

Se debe habilitar el complemento de ingres de la siguiente manera:

```bash
$ microk8s enable ingress
```