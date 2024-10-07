# Instalar metrics Server.
## Instalar metrics-server en minikube.
```
minikube addons list
minikube addons enable metrics-server
```
![image](https://github.com/user-attachments/assets/da1d80de-4566-4b0c-b785-e871909764bf)
![image](https://github.com/user-attachments/assets/064d180e-9331-48f2-8568-09f07c4642fa)

## Verificar si funciona las metricas de kubernetes.
```
kubectl get pods
kubectl top pod nombre-pod
```
![image](https://github.com/user-attachments/assets/47ef5a97-c6ba-459e-8d78-1133a400081b)

> [!IMPORTANT]
> De esta forma se instala desde minikube, pero para instalar en un cluster real debemos utilizar la docu oficial de metrics-server.
> https://github.com/kubernetes-sigs/metrics-server
