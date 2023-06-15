# KUBERNETES PATH LEARNING

## Kubernetes Path Learning

- [ ]  Instalar un clúster
- [ ]  Instalar CLI kubectl
- [ ]  instalar binario
- [ ]  conectarse a un cluster de un provider
- [ ]  kubectl apply y kubectl create DIFERENCIAS
- [ ]  crear namespace kubectl create namespace <nombre>
- [ ]  entender nodeport
- [ ]  entender loadbalancer
- [ ]  desplegar un loadbalancer external ip con un manifiesto deployment.yaml con imagen nginx

## ReplicaSets and Deployments

```bash
# CREAR UN NAMESPACE 
kubectl create namespace <nombre>
```

```bash
# describe el deployment
kubectl describe deployments deployment-1 --namespace=namespace-1
```

```bash
# entender
kubectl get pods
```

```bash
# entender
kubectl get pods -o wide
```

```bash
kubectl describe svc
```

```bash
kubectl describe deployments 
```

```bash
kubectl describe deployments deployment-1 --namespace=namespace-1
```

```bash
kubectl set image
```

```bash
kubectl set image deployment/deployment-1 nginx=nginx:1.16.1
```

```bash
#ROLLOUT AL ANTERIOR DEPLOYMENT

kubectl rollout history y undo
```

```bash
kubectl rollout history deployment/deployment-1 --namespace=namespace-1
```

```bash
kubectl rollout undo deployment/deployment-1 --namespace=namespace-1
```

## Services and Ingresses

- Que es un servicio
    - Motodo para exponer una aplicacion de red que esta corriendo en uno o mos pods en nuestro cluster
- Define un set de endpoints logicos y politicas de acceso de red de nuestro pod
- Tres tipos de servicios
    - ClusterIP
    - NodePort
    - Loadbalancer
    

![Untitled](KUBERNETES%20PATH%20LEARNING%20b9a636e8797c4212b589fe0d12c6f635/Untitled.png)

![Untitled](KUBERNETES%20PATH%20LEARNING%20b9a636e8797c4212b589fe0d12c6f635/Untitled%201.png)

- Que es un ingress
    - Es un objeto de la API de Kubernetes que maneja el acceso externo a nuestros servicios de nuestro cluster , tipicamente http
    - pueden proveer load balancing, terminacion ssl y name-based virtual hosting
    

![Untitled](KUBERNETES%20PATH%20LEARNING%20b9a636e8797c4212b589fe0d12c6f635/Untitled%202.png)

![Untitled](KUBERNETES%20PATH%20LEARNING%20b9a636e8797c4212b589fe0d12c6f635/Untitled%203.png)

![Untitled](KUBERNETES%20PATH%20LEARNING%20b9a636e8797c4212b589fe0d12c6f635/Untitled%204.png)

## Lab Services and Ingress Controller

Yaml Hello World Nginx

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-world-deployment
  namespace: namespace-1
  labels:
    type: webapp
spec:
  replicas: 1
  selector:
    matchLabels:
      type: webapp
  template:
    metadata:
      labels:
        type: webapp
    spec:
      containers:
      - name: webapp
        image: nginxdemos/hello
        ports:
        - containerPort: 80
        resources:
          requests:
            memory: "32Mi"
            cpu: "200m"
          limits:
            memory: "64Mi"
            cpu: "300m"
```

```bash
kubectl apply -f deployment.yaml
```

NGINX Ingress Controller by executing the below command,

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.1.2/deploy/static/provider/cloud/deploy.yaml
```

Wait for the ingress pods to come up and running.

```bash
kubectl get pods --namespace=ingress-nginx

```

We will now create an ingress resource declaratively that maps to <your_hostname>.127.0.0.1.sslip.io

```bash
kubectl create ingress hello-world-ingress --class=nginx --rule="<your_hostname>.127.0.0.1.sslip.io/*=hello-world-service:80" -n namespace-1

#funciona si el puerto lo mando al 8080 me di cuenta con un kubectl gtsvc --namespace=namespace1 vii que el servicio helloworld del la ip del cluster ip el puerto es 8080
```

Forward a local port to the ingress controller.

```bash
kubectl port-forward --namespace=ingress-nginx service/ingress-nginx-controller 8081:80
```

NOTAS

ocupe la external ip de servicio ingress-nginx

```bash
kubectl get svc --namespace=ingress-nginx
```

- [ ]  Configurar la red y el almacenamiento
- [ ]  Desplegar aplicaciones y servicios
- [ ]  Gestionar y escalar aplicaciones y servicios
- [ ]  Mantener la alta disponibilidad del clúster y las aplicaciones
- [ ]  Actualizar el clúster y las aplicaciones
- [ ]  Monitorear y depurar el clúster y las aplicaciones
- [ ]  Aprender sobre la seguridad de Kubernetes

1. Introducción a Kubernetes
    - ¿Qué es Kubernetes y por qué es importante?
    - Arquitectura de Kubernetes
    - Conceptos clave: pods, servicios, replicaset, despliegues, etc.
2. Instalación y configuración de Kubernetes
    - Instalación local con minikube o kind
    - Configuración de clústeres de Kubernetes en la nube (GKE, AKS, EKS)
3. Despliegue de aplicaciones en Kubernetes
    - Creación y administración de pods
    - Despliegue de aplicaciones con despliegues (deployments)
    - Configuración de servicios para acceder a las aplicaciones
4. Escalado y actualización de aplicaciones
    - Escalado horizontal y vertical de los pods
    - Actualización de aplicaciones sin tiempo de inactividad (rolling updates)
    - Rollbacks de aplicaciones en caso de errores
5. Configuración y gestión de almacenamiento en Kubernetes
    - Volumenes persistentes y almacenamiento en Kubernetes
    - Configuración de almacenamiento distribuido (StorageClasses)
    - Uso de almacenamiento externo (por ejemplo, servicios de almacenamiento en la nube)
6. Networking en Kubernetes
    - Configuración de redes y servicios en Kubernetes
    - Comunicación entre pods y servicios
    - Configuración de políticas de red y seguridad
7. Monitoreo y registro en Kubernetes
    - Implementación de monitoreo de clúster y aplicaciones
    - Uso de métricas y registros para analizar el rendimiento y solucionar problemas
    - Uso de herramientas como Prometheus, Grafana y Fluentd
8. Administración avanzada de Kubernetes
    - Gestión de roles y permisos (RBAC) en Kubernetes
    - Programación de tareas (CronJobs)
    - Configuración de recursos y límites de recursos
9. Escalado y alta disponibilidad en Kubernetes
    - Configuración de clústeres de alta disponibilidad
    - Uso de balanceadores de carga y servicios de tipo "LoadBalancer"
    - Configuración de tolerancia a fallos y recuperación automática
10. Despliegue continuo y automatización en Kubernetes
    - Integración de Kubernetes con herramientas de CI/CD
    - Automatización de despliegues y pruebas en Kubernetes
    - Estrategias de entrega continua en Kubernetes

Este plan de estudios te proporciona una estructura gradual para aprender Kubernetes, desde los conceptos básicos hasta temas más avanzados como escalado, alta disponibilidad y automatización. A medida que avanzas, te recomiendo practicar con ejemplos y proyectos reales para obtener experiencia práctica con Kubernetes. ¡Disfruta aprendiendo!

[Kubernetes - Guides](https://jamesdefabia.github.io/docs/)

[Kubernetes Up & Running: Dive into the Future of Infrastructure](https://tanzu.vmware.com/content/ebooks/kubernetes-up-running-dive-into-the-future-of-infrastructure)