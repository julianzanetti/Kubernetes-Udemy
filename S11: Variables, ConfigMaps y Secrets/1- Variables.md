# Variables.
## Ejemplo de mysql.yaml con variables.
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql-deploy
  labels:
    app: mysql
    type: db
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mysql
      type: db
  template:
    metadata:
      labels:
        app: mysql
        type: db
    spec:
      containers:
      - name: mysql-contenedor
        image: mysql
        env:
          - name: MYSQL_ROOT_PASSWORD
            value: kubernetes
          - name: MYSQL_USER
            value: usudb
          - name: MYSQL_PASSWORD
            value: usupass
          - name: MYSQL_DATABASE
            value: kubernetes
        ports:
        - containerPort: 3306
          name: db-port
```
```
kubectl apply -f var-mysql.yaml
kubectl get all
```
![image](https://github.com/user-attachments/assets/4a7fbc82-573b-4d7b-ae2b-966a8bdb21ab)

## Ingresamos dentro del contenedor.
```
kubectl exec -it mysql-deploy-f58599f64-flqrq bash
```
![image](https://github.com/user-attachments/assets/d6c0da83-00e6-4342-b52b-0e107c785e3a)

## Visualizamos las variables y ingresamos dentro del mysql con el usuario usudb.
```
printenv
mysql -u usudb -p kubernetes
```
![image](https://github.com/user-attachments/assets/6f86b2d0-6796-4736-a02d-c93bb7e2b81e)
![image](https://github.com/user-attachments/assets/8eaa0715-9452-45b0-b40b-79c135af9b9c)

## Mostrar la bd kubernetes.
```
show databases;
```
![image](https://github.com/user-attachments/assets/b39d490b-3cfd-4d17-b98a-425c5e665c0f)

