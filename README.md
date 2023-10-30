# microk8s-app
Este repositorio de código esta realizado específicamente para validar habilidades y destrezas obtenidas durante los años de trabajando. Se implementara la codificación completa empezando con la configuración de un kubernetes (microk8s) instalado en ubuntu y se desarrollará una app sencilla usando frontend vue3 y backen en node.js, rust y java (Spring Boot). Se uzaran herramientas para la observabilidad (pgadmin4, kibana, new relic) y para ayudar el rol de devops implementaremos (jenkins, sonarqube), en la parte operativa trabajaremos con un sistema de base de datos postgreSQL, un broker de mensajeria RabbitMQ, una base de datos en memoria redis y finalmente usaremos una base de datos mongoDB.

## Sobre la instalación de microk8s instalado en Ubuntu 22.04.3 LTS

La documentación, sobre la instalación y la configuración de microk8s en el sistema operarivo ubuntu y otras configuraciones de microk8s usadas se encuentran disponibles en la carpeta microk8s-config

## Empezamos ejecutando Jenkins

Ejecutamos el archivo ```main.yaml``` el cual esta ubicado en la carpeta jenkins:

```bash
$ kubectl apply -f jenkins/main.yaml
```

Esto crea:

```bash
namespace/devops created
serviceaccount/jenkins-admin created
clusterrole.rbac.authorization.k8s.io/jenkins-admin created
clusterrolebinding.rbac.authorization.k8s.io/jenkins-admin created
persistentvolume/jenkins-pv-volume created
persistentvolumeclaim/jenkins-pv-claim created
deployment.apps/jenkins created
service/jenkins-service created
ingress.networking.k8s.io/jenkins-ingress created
```

## Consultamos el log del contenedor de jenkins para obtener la clave

Podemos obtener el nombre del contenedor con el comando: ```kubectl get pod -n devops```

```bash
$ kubectl logs jenkins-f6b8c4467-jhkxz -n devops
```

copiamos la clave para instalación del jenkins

## agregamos nuestro nombre de dominio en el archivo de hosts

El archivo de Host para Ubuntu en este caso ```/etc/hosts``` y agregamos el siguiente nombre de dominio

```bash
# /etc/hosts
127.0.0.1       app.jenkins.tech
```

ahora podemos acceder a la instalación de jenkins en [http://app.jenkins.tech](http://app.jenkins.tech)

