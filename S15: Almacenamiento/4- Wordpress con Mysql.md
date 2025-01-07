# Ejemplo: Wordpress con Mysql.
## Preparacion del entorno.
### Utilizaremos un un master y dos esclavos:
![image](https://github.com/user-attachments/assets/9134c8f7-d781-49ba-904d-718b4077c8af)

### Crearemos un workdir con dos directorios (esto se realiza en el master y en los dos esclavos):
```
mkdir /home/kubernetes/datos/mysql
mkdir /home/kubernetes/datos/wordpress
```
![image](https://github.com/user-attachments/assets/ed1aa37e-15f6-49d6-88bc-6ad10626b457)

### Configuramos los permisos de NFS para los dos directorios en el /etc/exports.
![image](https://github.com/user-attachments/assets/d744babc-b75e-43b8-a6be-1ae145e56347)

### Rebotamos el kernel.
```
systemctl restart nfs-kernel-server
```
![image](https://github.com/user-attachments/assets/8eb6ec03-c34d-4369-9f98-f79932079797)

### Montamos en los esclavos los workdir del master.
```
mount -t nfs ip-master:/home/kubernetes/datos/mysql /home/kubernetes/datos/mysql
mount -t nfs ip-master:/home/kubernetes/datos/wordpress /home/kubernetes/datos/wordpress
```
![image](https://github.com/user-attachments/assets/00e87b3f-7be3-4610-be05-2bff9fd73361)

## Crear el PV y PVC.
### Ejemplo archivo PV para wordpress.
```
#########################
## PV para WORDPRESS  ###
########################
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-wordpress
spec:
  capacity:
    storage: 25Gi
  accessModes:
    - ReadWriteMany
  persistentVolumeReclaimPolicy: Recycle
  storageClassName: wordpress
  nfs:
    path: /home/kubernetes/datos/wordpress
    server: ip-master
```

### Ejemplo archivo PV para mysql.
```
#####################
## PV para MySQL  ###
#####################
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-mysql
spec:
  capacity:
    storage: 25Gi
  accessModes:
    - ReadWriteMany
  persistentVolumeReclaimPolicy: Recycle
  storageClassName: mysql
  nfs:
    path: /home/kubernetes/datos/mysql
    server: ip-master
```
![image](https://github.com/user-attachments/assets/9ce881de-0d06-4fb6-83ea-7dfc61dfbab9)

### Ejemplo archivo PVC wordpress.
```
###########################
## CLAIM PARA  WORDPRESS ##
###########################
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-wordpress
spec:
  storageClassName: wordpress
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: 20Gi
```

### Ejemplo archivo PVC para mysql.
```
######################
## CLAIM PARA MYSQL ##
######################
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-mysql
spec:
  storageClassName: mysql
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: 20Gi
```
![image](https://github.com/user-attachments/assets/28e00164-2a04-435f-a690-7f40fa8c5dea)
![image](https://github.com/user-attachments/assets/7580a82a-bc1a-403d-8cf9-03add4dc19a8)

## Crear el deploy de Wordpress y Mysql.
### Ejemplo de archivo deploy para wordpress.
```
#############################
## SERVICIO PARA WORDPRESS ##
#############################
apiVersion: v1
kind: Service
metadata:
  name: wordpress
  labels:
    app: wordpress
spec:
  ports:
    - port: 80
  selector:
    app: wordpress
    tier: frontend
  #type: LoadBalancer
  type: NodePort
---
###############################
## DEPLOYMENT PARA WORDPRESS ##
###############################
apiVersion: apps/v1
kind: Deployment
metadata:
  name: wordpress
  labels:
    app: wordpress
spec:
  selector:
    matchLabels:
      app: wordpress
      tier: frontend
  strategy:
    type: Recreate
  template:
    metadata:
      labels:
        app: wordpress
        tier: frontend
    spec:
      containers:
      - image: wordpress:4.8-apache
        name: wordpress
        env:
        - name: WORDPRESS_DB_HOST
          value: mysql
        - name: WORDPRESS_DB_PASSWORD
          value: password
        ports:
        - containerPort: 80
          name: wordpress
        volumeMounts:
        - name: wordpress-persistent-storage
          mountPath: /var/www/html
      volumes:
      - name: wordpress-persistent-storage
        persistentVolumeClaim:
          claimName: pvc-wordpress 
```
![image](https://github.com/user-attachments/assets/9c483bd7-9f03-4c12-b39a-06c6c3b4b714)

### Ejemplo de archivo deploy para Mysql.
```
#####################
## SERVICIO MYSQL  ##
#####################
apiVersion: v1
kind: Service
metadata:
  name: mysql
  labels:
    app: wordpress
spec:
  ports:
    - port: 3306
  selector:
    app: wordpress
    tier: mysql
  clusterIP: None
---
########################
## DEPLOYMENT  MYSQL  ##
########################
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql
  labels:
    app: wordpress
spec:
  selector:
    matchLabels:
      app: wordpress
      tier: mysql
  strategy:
    type: Recreate
  template:
    metadata:
      labels:
        app: wordpress
        tier: mysql
    spec:
      containers:
      - image: mysql:5.6
        name: mysql
        env:
        - name: MYSQL_ROOT_PASSWORD
          value: password
        ports:
        - containerPort: 3306
          name: mysql
        volumeMounts:
        - name: mysql-persistent-storage
          mountPath: /var/lib/mysql
      volumes:
      - name: mysql-persistent-storage
        persistentVolumeClaim:
          claimName: pvc-mysql
```
![image](https://github.com/user-attachments/assets/3d156a3d-e9db-4295-9774-e2c393e7b1bd)

## Ingresar al Wordpress por web.
> [!NOTE]
> Se ingresa con la IP del master y el puerto del servicio de kubernetes
> ![image](https://github.com/user-attachments/assets/e47546df-3718-4777-9c8d-6a8ba7bfe914)
![image](https://github.com/user-attachments/assets/5b5d87ae-3cbb-4a62-bda0-8f1c253064f1)

## Instalar wordpress y verificar que se haya creado la BD.
> [!NOTE]
> Si ingresamos desde cualquier esclavo, la BD tiene que aparecer creada.
> 
```
cd /home/kubernetes/datos/mysql
```
![image](https://github.com/user-attachments/assets/251e4a50-57a5-4a3d-81ee-0bad2cc8075e)
![image](https://github.com/user-attachments/assets/e61d0570-5c11-4318-be20-e3a194344061)
