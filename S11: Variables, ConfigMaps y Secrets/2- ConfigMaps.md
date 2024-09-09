# ConfigMaps.
## ConfigMap de forma imperativa.
```
kubectl create configmap cm1 --from-literal=usuario=usu1 --from-literal=password=pass1
kubectl get cm
kubectl describe cm cm1
```
![image](https://github.com/user-attachments/assets/46aadda0-4136-4564-8cb8-0f8888d4c988)

## ConfigMap desde ficheros.
### Creamos un fichero de mysql.properties
```
MYSQL_ROOT_PASSWORD=kubernetes
MYSQL_USER=usudb
MYSQL_PASSWORD=usupass
MYSQL_DATABASE=kubernete
```
### Creamos el configmap a traves de este fichero.
```
kubectl create configmap datos-mysql --from-file=mysql.properties
kubectl get cm
kubectl describe cm datos-mysql
```
![image](https://github.com/user-attachments/assets/84f3a252-d296-46a7-bfe2-3e23b508f454)
> [!WARNING]
> Al utilizar el configmap de esta forma, vemos que toma como clave el nombre del fichero y el valor todos lo que tengamos dentro del fichero.

### Utilizamos dentro de un POD.
```
apiVersion: v1
kind: Pod
metadata:
  name: pod1
  labels:
    app: mysql
spec:
  containers:
  - name: busybox-contenedor
    image: busybox
    command: ["sh", "-c", "while true; do env; sleep 30; done"]
    env:
      - name: DATOS-MYSQL
        valueFrom:
          configMapKeyRef:
            name: datos-mysql
            key: mysql.properties
```
![image](https://github.com/user-attachments/assets/0649f779-2d67-435f-bf5f-0aeb054eaacf)
![image](https://github.com/user-attachments/assets/c2530b55-f209-4cbb-9cad-5c74b7b70c55)

## Cargar variables desde un fichero.
```
kubectl create configmap mysql-properties --from-env-file mysql.properties
```
![image](https://github.com/user-attachments/assets/10e93b52-1213-4f5e-bffb-9e27f5b36120)
```
apiVersion: v1
kind: Pod
metadata:
  name: pod1
  labels:
    app: myapp
spec:
  containers:
  - name: busybox-contenedor
    image: busybox
    command: ["sh", "-c", "while true; do env; sleep 30; done"]
    envFrom:
      - configMapRef:
          name: mysql-properties
```
![image](https://github.com/user-attachments/assets/71810456-b96e-457d-ba1f-861ba3113ed9)
> [!NOTE]
> De esta forma vemos que se crean las variables respetando la clave=valor que hemos configurado en nuestro fichero.
