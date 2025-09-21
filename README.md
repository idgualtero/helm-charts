### Grupo 3

#####

# Kubernetes Minikube

## Instalación de Minikube

### Paso 1: Instalar Minikube

```bash
choco install minikube

# O descargar desde: https://minikube.sigs.k8s.io/docs/start/
```

### Paso 2: Instalar kubectl

```bash
choco install kubernetes-cli

# O descargar desde: https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/
```

## Uso de Minikube con la Aplicación

### Paso 1: Iniciar Minikube

```bash

minikube start --driver=docker --memory=2048 --cpus=2
minikube status
```

### Paso 2: Revisar status pods y services

```bash
kubectl get pods
kubectl get services
```

### Paso 3: Acceder a la aplicación

```bash
minikube service pedido-app-backend --url
minikube service pedido-app-backend
```

### Paso 4: Ver logs

```bash
kubectl logs -f deployment/pedido-app-backend
kubectl exec -it <nombre-del-pod> -- /bin/bash
```

### Paso 5: Monitorear el escalado automático

```bash
kubectl get hpa
kubectl describe hpa pedido-app-backend
kubectl top pods
```

## Comandos útiles de Minikube

```bash
minikube stop
minikube start
minikube delete
minikube status
minikube service list
```

## Solución de problemas comunes

### Si la aplicación no responde:

```bash
kubectl get pods
kubectl logs deployment/pedido-app-backend
kubectl describe service pedido-app-backend
```

# Comandos para genera helm

Empaquetar en la carpeta charts

## Acceder a la carpeta carts

```
cd charts
```

## Genera los archivos gtz de postgres que son dependencia

```
helm dependency update pedido-app
```

## genera el tgz de la aplicacion

```
helm package pedido-app
```

## Genera el index.yaml

```
helm repo index . --url https://idgualtero.github.io/helm-charts/charts
```

## Agregar al cluste de Helm

```
helm repo add pedido-app https://idgualtero.github.io/helm-charts/charts
```

```
helm repo update
```

## Si se quiere borrar algo de helm

```
helm repo remove pedido-app
```

### Proceso ArgoCD

### Instalación de ArgoCD en Minikube

```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

### Acceso a ArgoCD

```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

## Obtener pwd de ArgoCD

```bash
kubectl -n argocd get secret argocd-initial-admin-secret \
-o jsonpath="{.data.password}" | base64 --decode
```

### Aplicar yaml

```bash
kubectl apply -f application.yaml -n argocd
```

### Proceso Jenkins

### Instalacion

```bash
sudo apt update
sudo apt install openjdk-17-jdk -y
wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins.io/debian binary/ > \
    /etc/apt/sources.list.d/jenkins.list'
sudo apt update
sudo apt install jenkins -y
```

### Iniciar y habilitar Jenkins

```bash
sudo systemctl start jenkins
sudo systemctl enable jenkins
```

### Obtener pwd

```bash
Usuario defecto: admin
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```
