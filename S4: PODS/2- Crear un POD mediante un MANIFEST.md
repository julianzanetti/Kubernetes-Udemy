# Crear un POD mediante un MANIFEST.
## Vamos a crear nuestro Dockerfile para luego crear la imagen.
```
##Descargamos UBUNTU
FROM ubuntu

##Actualizamos el sistema
RUN apt-get update

##Instalamos NGINX
RUN apt-get install -y nginx

##Creamos un fichero index.html en el directorio por defecto de nginx
RUN echo 'Ejemplo de POD con KUBERNETES y YAML' > /var/www/html/index.html

##Arrancamos NGINX a través de ENTRYPOINT para que no pueda ser modificado en la creación del contenedor
ENTRYPOINT ["/usr/sbin/nginx", "-g", "daemon off;"]

##Exponemos el Puerto 80
EXPOSE 80
```

## Creamos la imagen y subirlo a nuestro DockerHUB.
![image](https://github.com/user-attachments/assets/0bcf7dfb-4e1a-4152-93b4-2e6a1ae4a940)
![image](https://github.com/user-attachments/assets/47b13c1a-a42f-454a-98c9-bd39ad41f6b9)

## Crear el yaml para levantar un POD de esta imagen.
```
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    zone: prod
    version: v1
spec:
  containers:
   - name: nginx   
     image: julianzanetti/nginx1:v1
```
![image](https://github.com/user-attachments/assets/b9f7ac84-fac8-4954-a452-bc241cf76a9c)

## Vamos a levantar nuestro POD indicado en el yaml y verificamos que este levantado.
```
kubectl create -f nombre.yaml
kubectl get pods
```
![image](https://github.com/user-attachments/assets/4e7b92e3-f146-48d5-9660-1f01e9b9fc02)

## Visualizar nuestro POD en la web.
```
kubectl port-forward nombre_pod puerto-ingreso:puerto-pod
```
![image](https://github.com/user-attachments/assets/86482313-0d42-48b9-911f-9c9f741ddcc7)
![image](https://github.com/user-attachments/assets/f01f6b93-a9ae-483e-ae41-09b9f700757e)

