# Instalar Minikube con Docker
## Requisitos:
1. 2 CPUs o mas.
2. 2 GB minimo de ram.
3. 20 GB libre de espacio en disco.
4. Contenedor o Maquina virtual: Docker, VirtualBox, Hyper-V, Podman, etc.

## Descargamos el binario.
```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
```
![image](https://github.com/user-attachments/assets/15bf4f35-2987-44ba-bb34-0583db60467b)

## Instalamos el binario descargado.
```
install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64
```
![image](https://github.com/user-attachments/assets/4afc8f25-ae64-4416-a955-d846899d0a0f)

## Verificamos que se haya instalado correctamente.
```
minikube version
```
![image](https://github.com/user-attachments/assets/d374658f-efb6-4943-9d74-ab400533ae9e)

## Arrancamos el minikube con el RunTime de Docker.
```
minikube start --driver=docker
```
![image](https://github.com/user-attachments/assets/4c7316ac-edd6-4d69-b62f-0b48ba2ab36b)

## Verificamos que haya arrancado correctamente.
```
minikube status
```
![image](https://github.com/user-attachments/assets/4ed6e673-94a3-46fa-8d72-b5a25b18250d)
