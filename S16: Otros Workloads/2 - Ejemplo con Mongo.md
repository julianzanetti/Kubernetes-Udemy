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

## Crear el StatefulSet.
### Archivo de StatefulSet.
```
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: mongo
spec:
  selector:
    matchLabels:
      app: db
      name: mongodb
  serviceName: mongodb-svc #Servicio headless
  replicas: 3
  template:
    metadata:
      labels:
        app: db
        name: mongodb    
    spec:
      terminationGracePeriodSeconds: 10  
      containers:
      - name: mongo
        image: mongo:3.6        
        command: 
          - mongod
        args: 
          - --bind_ip=0.0.0.0
          - --replSet=rs0 #Nombre del replica set. Todos los miembros dle cluster usan este nombre
          - --dbpath=/data/db          
        livenessProbe:
            exec:
              command:
                - mongo
                - --eval
                - "db.adminCommand('ping')"
        ports:
        - containerPort: 27017
        volumeMounts:
        - name: mongo-storage
          mountPath: /data/db    
  volumeClaimTemplates:
    - metadata:
        name: mongo-storage      
      spec:
        storageClassName: estado
        accessModes: ["ReadWriteOnce"]
        resources:
          requests:
            storage: 1Gi
```
![image](https://github.com/user-attachments/assets/ff6a4012-6eb1-46b3-823d-458431791214)

## Arrancar las replicas de mongo (sincronizar).
> [!NOTE]
> Esto solamente es para sincronizar las replicas que tengamos en mongo. Recordar ver si nuestra software de BD permite esto.
```
rs.initiate({_id: "rs0", version: 1, members: [{ _id: 0, host :"mongo-0.mongodb-svc:27017" },{ _id: 1, host: "mongo-1.mongodb-svc:27017" }, { _id: 2, host: "mongo-2.mongodb-svc:27017" } ]});
```
![image](https://github.com/user-attachments/assets/599e8913-3d07-48d6-b187-c9d0d58212c8)

### Levantamos el cliente web de mongo y ingresamos.
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mongo-express
  labels:
    app: web
    name: mongo-express
spec:
  replicas: 1
  selector:
    matchLabels:
      app: web
      name: mongo-express
  template:
    metadata:
      labels:
         app: web
         name: mongo-express
    spec:
       containers:
       - name: mongo-express
         image: mongo-express
         env:
         - name: ME_CONFIG_MONGODB_SERVER
           value: mongo-0.mongodb-svc
         ports:
           - containerPort: 8081
---
apiVersion: v1
kind: Service
metadata:
  name: mongo-express-svc
spec:
  type: LoadBalancer
  selector:
    app: web
    name: mongo-express
  ports:
  - protocol: TCP
    port: 80
    targetPort: 8081
```
![image](https://github.com/user-attachments/assets/696634ab-69a8-411f-a6e8-8307fc237261)
![image](https://github.com/user-attachments/assets/39b816cd-580b-4e5c-be72-4686742d8a2b)

### Creamos una database y verificamos que se compartan en las replicas.
![image](https://github.com/user-attachments/assets/823e20e0-96c1-4773-b669-aefe0025c022)
### Mongo-0
![image](https://github.com/user-attachments/assets/9ee533ea-aed7-461d-8626-491e4b7f1c68)
### Mongo-1
![image](https://github.com/user-attachments/assets/8d3008d6-d7ca-4a90-b006-9628bf5296dc)
