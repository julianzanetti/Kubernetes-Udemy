# Recreate.
## Modificamos nuestro manifest para que el roll sea de tipo recreate.
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-d
  labels:
    estado: "1"
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 10
  strategy:
    type: Recreate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
  minReadySeconds: 3
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx
        ports:
        - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: nginx-svc
  labels:
    app: nginx
spec:
  selector:
    app: nginx
  type: NodePort
  ports:
  - port: 80
    nodePort: 31000
    protocol: TCP

```
![image](https://github.com/user-attachments/assets/c530d2b4-ad04-4af9-adb4-8599138ef752)

## Modificamos la version de la imagen y visualizar rapidamente los pods.
```
kubectl get pods -w
```
![image](https://github.com/user-attachments/assets/18ebf851-435b-470b-8f65-6b38fb4e0128)
![image](https://github.com/user-attachments/assets/6802c4b6-e7f8-4235-8df9-182a8e06c177)
