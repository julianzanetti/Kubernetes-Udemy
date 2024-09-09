# Ejemplo MYSQL con Configmap
## Creamos el configmap.
```
kubectl create configmap mysql-properties --from-env-file mysql.properties
kubectl describe cm mysql-properties
```
![image](https://github.com/user-attachments/assets/0a228d62-dd83-40ba-b5a6-724cdfff0357)

## Creamos nuestro yaml.
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
        envFrom:
          - configMapRef:
              name: mysql-properties
        ports:
        - containerPort: 3306
          name: db-port
```
```
kubectl apply -f var2-mysql.yaml
kubectl get pod
```
![image](https://github.com/user-attachments/assets/fa91faee-e8ef-431c-b6c7-46f977f9e409)

## Ingresamos dentro del contenedor y visualizamos las variables.
```
kubectl exec -it mysql-deploy-7865b84486-jlvc5 bash
```
![image](https://github.com/user-attachments/assets/559fd66d-ebb9-4ce5-983f-472a7168a6c4)

## Visualizar la bd llamada kubernetes.
![image](https://github.com/user-attachments/assets/e1ddf05b-f9b3-4299-9620-c31dd2d2dbfe)
