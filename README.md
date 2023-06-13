# k8s-notes

# Exportar configuracion k8s manejado 
```bash
export KUBECONFIG=vke-8b4ee69e-2c6a-4b07-a545-5d7c5bee0df7.yaml
```
# Contenedor con CURL oficial docker hub

https://hub.docker.com/r/curlimages/curl
https://hub.docker.com/r/nginxdemos/hello


# ver servicios pod y namesapces
```bash
kubectl get all
```
# ver mas info servicios
```bash
kubectl describe svc <service_name>
```
# YAML desplegar un pod de curl para testear en cluster de k8s

apiVersion: v1
kind: Pod
metadata:
  name: ubuntu
spec:
  containers:
    - name: ubuntu
      image: curlimages/curl:8.1.2
      command: ["sleep", "infinity"]

# aplicar cambios
kubectl apply -f curl.yaml

# Entrar en terminal interactiva en contenedor
 kubectl exec -it ubuntu sh
 
 # Obtener mas informacion de un servicio 
 
 root@jenkins8ram:~/kubeconfig# kubectl describe svc example
 
 
  # YAML con loadbalancer con imagen de nginx escucha puerto 80 

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello
spec:
  replicas: 3
  selector:
    matchLabels:
      role: hello
  template:
    metadata:
      labels:
        role: hello
    spec:
      containers:
      - name: hello
        image: nginxdemos/hello
        ports:
        - containerPort: 80

---
apiVersion: v1
kind: Service
metadata:
  name: hello
spec:
  type: LoadBalancer
  ports:
  - port: 80
    targetPort: 80
  selector:
    role: hello```

