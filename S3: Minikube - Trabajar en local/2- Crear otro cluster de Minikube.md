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
