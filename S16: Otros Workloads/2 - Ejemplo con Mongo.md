# Ejemplo con Mongo.
## Crear SC y Servicio.
### Archivo SC de mongo.
```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
   name: estado
provisioner: k8s.io/minikube-hostpath
parameters:
  type: pd-ssd
```
![image](https://github.com/user-attachments/assets/a8321495-adff-40fd-8ade-d47cd922d74e)

### Archivo Servicio de Mongo.
```
apiVersion: v1
kind: Service
metadata:
  name: mongodb-svc
  labels:
    app: db
    name: mongodb
spec:
  ports:
  - port: 27017
  clusterIP: None 
  selector:
    app: db
    name: mongodb 
```
![image](https://github.com/user-attachments/assets/1a6b8431-a5bc-4234-8e27-85dc3fbd716c)
