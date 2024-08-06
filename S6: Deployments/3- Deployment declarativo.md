# Crear un deployment declarativo.
## Creamos nuestro primer yaml del deploy con imagen de nginx.
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deploy
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 2
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        resources:
        ports:
        - containerPort: 80
```
![image](https://github.com/user-attachments/assets/df0fe3ab-e7c4-4b1e-a181-778f2e0f43c4)

## Levantamos este deploy.
```
kubectl apply -f deploy_nginx.yaml
```
![image](https://github.com/user-attachments/assets/067597e8-80f0-4b2e-b3eb-2e3ba9353007)

## Visualizar el deploy, los pods y el replicaset.
```
kubectl get deploy
kubectl get pods
kubectl get rs
```
![image](https://github.com/user-attachments/assets/03cb7076-ae5e-4d8c-84f7-bbd5d49fd675)

### Otra forma
```
kubectl get pods,deploy,rs
```
![image](https://github.com/user-attachments/assets/170e0504-bd2d-4e57-8232-1112cc393d92)

## Buscar el pod por las label
```
kubectl get pods -l app=nginx
```
![image](https://github.com/user-attachments/assets/c6503922-a43e-4867-a28a-b3a52fa5e436)

