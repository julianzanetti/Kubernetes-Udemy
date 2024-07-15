# Crear otro cluster de Minikube con multiples nodos.
## Podemos verificar o listar los cluster que tenemos creados con este comando:
```
minikube profile list
```
![image](https://github.com/user-attachments/assets/d6f21a90-5c24-4cdb-b556-423dc1a874e9)

## Vamos a crear otro cluster llamado clusterDesa con dos nodos y volvemos a listar los cluster.
```
minikube start --driver=docker -p clusterDesa --nodes=2
minikube profile list
```
![image](https://github.com/user-attachments/assets/549bb722-9cfb-4300-931c-c70f8d8e42f0)

## Vamos a aumentar la memoria del cluster recien creado.
```
minikube config set memory 4G -p clusterDesa
```
![image](https://github.com/user-attachments/assets/e62af5b4-9e69-4613-82ec-6bbb66709ebe)

## Vamos a cambiar al cluster recien creado.
```
minikube profile clusterDesa
minikube profile
```
![image](https://github.com/user-attachments/assets/e25594ea-0cef-4898-b19a-1e99f25d1cf1)

## Verificar cuantos nodos estan corriendo.
```
kubectl get nodes
```
![image](https://github.com/user-attachments/assets/ede992fb-7620-41bb-894d-d436ea098f9a)

## Cambiar al perfil predeterminado y consultar nuevamente.
```
minikube profile minikube
kubectl get nodes
```
![image](https://github.com/user-attachments/assets/1a50a7a2-d9c7-49be-98c2-fa4f38cbb3ee)
