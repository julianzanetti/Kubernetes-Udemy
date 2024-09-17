# Secrets.
## Tipos de Secrets.
- `Opaque|Genericos`: Tipo por defecto que contiene cualquier informacion que queramos incluir y proteger. Son como los CM pero estos estan codificados en base64
- `Service Account Token`: Almacena un token para un service account. Basicamente almacena una identidad para los procesos dentro de un POD.
- `Docker Config`: Almacena las credenciales necesarias para poder acceder a un registro privado Docker.
- `Basic Authentication`: Credenciales que se utilizan para autentificacion basica. Contiene username y password.
- `SSH`: Almacena las credenciales para acceder por SSH. Vamos a necesitar la propiedad denominada "ssh-privatekey".
- `TLS`: Almacena un certificado y su clave asociada que se utilizan normalmente para TLS. Debemos tener el "tls.key" y "tls.crt".

## Secret de tipo generico.
```
kubectl create secret generic passwords --from-literal=pass-root=devuser --from-literal=pass-usu=kubernetes
kubectl get secret
```
![image](https://github.com/user-attachments/assets/88f42f69-a4d3-45d7-b200-a32f19049b38)

### Creamos un configmap con el nombre de la bd y usuario.
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: datos-mysql-env
  namespace: default
data:
  MYSQL_DATABASE: kubernetes
  MYSQL_USER: usudb
```
![image](https://github.com/user-attachments/assets/40d6b532-86e0-48ee-8833-d8bb73c15926)
> [!NOTE]
> Esto nos sirve para ver que podemos mezclar los ConfigMaps con los Secrets.

### Creamos un deploy de MYSQL y utilizamos el CM y secret.
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
        - name: mysql
          image: mysql
          ports:
            - containerPort: 3306
              name: db-port
          env:
            - name: MYSQL_ROOT_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: passwords
                  key: pass-root

            - name: MYSQL_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: passwords
                  key: pass-usu

            - name: MYSQL_USER
              valueFrom:
                configMapKeyRef:
                  name: datos-mysql-env
                  key: MYSQL_USER
            
            - name: MYSQL_DATABASE
              valueFrom:
                configMapKeyRef:
                  name: datos-mysql-env
                  key: MYSQL_DATABASE
```
![image](https://github.com/user-attachments/assets/8cfc0fbf-d983-4fbb-b6cf-31b9811249b0)

### Ingresamos al POD y verificamos si estan las pass configuradas en el Secret.
```
kubectl exec -it mysql-deploy-78f6cfbf84-m28bw bash
```
![image](https://github.com/user-attachments/assets/cdcc419e-dbff-407e-8e1e-f0f864ccb288)

### Probamos las credenciales y mostramos las bd dentro del mysql.
```
mysql -u usudb -p kubernetes
show databases;
```
![image](https://github.com/user-attachments/assets/fe24eff4-5d21-4325-8625-6aaab2345389)
