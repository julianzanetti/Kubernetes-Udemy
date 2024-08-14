# Crear un Servicio de forma declarativa.
## Creamos nuestro Dockerfile:
```
##Descargamos una versión concreta de UBUNTU
FROM ubuntu:latest
##Actualizamos el sistema
RUN apt update && apt upgrade -y
##Instalamos HTTPD Apache 2
RUN apt-get install apache2 -y
##Creamos un fichero index.html en el directorio por defecto de apache
ADD web /var/www/html
##Exponemos el Puerto 80
EXPOSE 80
##Arrancamos Apache a través de ENTRYPOINT para que no pueda ser modificado en la creación del contenedor
CMD /usr/sbin/apachectl -D FOREGROUND
```
![image](https://github.com/user-attachments/assets/0a9aa793-8c72-4361-9551-02e400187945)

```
docker build -t kubertenes-web .
```
![image](https://github.com/user-attachments/assets/f7111342-bbaa-4725-82af-09691a0e619d)

## Iniciamos un contenedor con la imagen recien creada.
```
docker run --name=kube-web1 -p 8080:80 -d kubernetes-web
```
![image](https://github.com/user-attachments/assets/618f2446-ae2f-4d9d-85a1-a812da239e54)

## Visualizar que funcione correctamente, luego borrarlo.
![image](https://github.com/user-attachments/assets/23042d84-1bc0-43c1-929e-d8397d91c08e)

## Creamos nuestro yaml para el deploy y servicio.
```
#############
# DEPLOYMENT  
#############
apiVersion: apps/v1 
kind: Deployment
metadata:
  name: web-deploy
spec:
  selector:
    matchLabels:
      app: web
  replicas: 2
  template:
    metadata:
      labels:
        app: web
    spec:
      containers:
      - name: apache
        image: julianzanetti/kubernetes-web:latest
        ports:
        - containerPort: 80
---

#############
# SERVICIO  
#############
apiVersion: v1
kind: Service
metadata:
  name: web-svc
  labels:
     app: web
spec:
  type: NodePort
  ports:
  - port: 80
    nodePort: 30002
    protocol: TCP
  selector:
     app: web
```
![image](https://github.com/user-attachments/assets/c251a123-2d2b-494a-887a-3e8f7dc312ab)

## Levantamos nuestro servicio.
```
kubectl apply -f kube-web.yaml
kubetcl get all
```
![image](https://github.com/user-attachments/assets/da53aa48-f716-42b7-af7c-57ce5cd2529b)

## Visualizamos en la web.
### Si utilizamos minikube realizar primero un tunel al cluster.
```
minikube service web-svc
```
![image](https://github.com/user-attachments/assets/392fb97b-bab4-4be1-b547-6330a07b717e)
![image](https://github.com/user-attachments/assets/d84f5392-eddf-4a55-a90f-eec9d27e2f49)
