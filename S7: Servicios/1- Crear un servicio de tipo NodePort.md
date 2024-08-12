# Crear un servicio de tipo NodePort.
## Crear un deploy con la imagen de apache.
```
kubectl create deployment apache1 --image=httpd
kubectl get all
```
![image](https://github.com/user-attachments/assets/1e8e3b39-1711-4921-8079-2fef4d66c823)

## Crear el servicio nodeport para el pod.
```
kubectl expose deploy apache1 --port=80 --type=NodePort
```
![image](https://github.com/user-attachments/assets/6eda7f03-46a9-4771-a940-b46d18ea69a2)

## Listar nuestro servicio creado.
```
kubectl get svc
```
![image](https://github.com/user-attachments/assets/e9f7df37-e803-46c9-8df3-d82ce47f8803)

## Probamos ingresar por fuera.
### - Como estoy en minikube primero necesitamos realizar un tunel al cluster.
```
minikube service apache1
```
![image](https://github.com/user-attachments/assets/82d27572-a73a-49ef-8ac7-56803c913275)

### - Ingresamos.
![image](https://github.com/user-attachments/assets/d7eab304-41a9-454e-acca-8a55d32a41f4)
