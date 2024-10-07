# Configurar la memoria y cpu de un Deployment.
## Ejemplo de un deploy asignando recursos.
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx
  labels:
    estado: "1"
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 5
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        resources:
          limits:
            memory: "500Mi"
            cpu: "2"
          requests:
            memory: "100M"
            cpu: "0.5"
        ports:
        - containerPort: 80

```
![image](https://github.com/user-attachments/assets/cf9a3d34-6b4d-4b0a-99c3-e1e8b3a11f25)

> [!IMPORTANT]
> Ver la documentacion oficial de Kubernetes para asignar los valores correctos tanto de CPU como Memoria.
> https://kubernetes.io/es/docs/concepts/configuration/manage-resources-containers/

## Corroborar si tomo la configuracion correspondiente.
```
kubectl describe deploy nginx
```
![image](https://github.com/user-attachments/assets/09a4f113-e6f8-41b8-8d98-f4bf9fde72ee)

