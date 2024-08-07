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

### Otra forma
```
kubectl get pods,deploy,rs -l app=nginx
```
![image](https://github.com/user-attachments/assets/96bcf4dc-e0c1-4328-95ce-f706f7bf7f27)

## Agregar una label al deploy y visualizarla.
![image](https://github.com/user-attachments/assets/7d0f2342-63ad-4cbf-a0ca-cbcf39b981b9)
```
kubectl apply -f deploy_nginx.yaml
kubectl get pods,deploy,rs -l app=nginx
```
![image](https://github.com/user-attachments/assets/679d0cfc-2107-4953-96b6-81132e657df8)

## Editar la cantidad de replicas de nuestro deploy sin modificar el yaml.
```
kubectl edit deploy nginx-deploy
```
![image](https://github.com/user-attachments/assets/785620ad-c014-4c29-9dc8-6787afed0c2b)
![image](https://github.com/user-attachments/assets/325473d0-94c6-4070-82c0-f7698c0658b2)

```
kubectl get deploy
```
![image](https://github.com/user-attachments/assets/44112937-3543-463f-ae70-41474a35b937)
