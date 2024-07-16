# Dashboard, parar y borrar un cluster en Minikube.md
## Ingresar al dashboard.
```
minikube dashboard
```
![image](https://github.com/user-attachments/assets/9ddd5bfe-1e56-44f8-8c5b-65ee50c6189b)
![image](https://github.com/user-attachments/assets/b609c8a1-f30a-4bde-9465-0545d4aefdfe)

## Listar nuestros cluster y desde el predeterminado levatar los otros.
```
minikube profile list
minikube start -p clusterDesa
```
![image](https://github.com/user-attachments/assets/a64e6606-8f33-45c0-a4c3-7048c981f139)
![image](https://github.com/user-attachments/assets/44445d18-88cc-4acc-9f6f-e565ff013433)

## Vamos a stopear el cluster que recien levantamos.
```
minikube stop -p clusterDesa
```
![image](https://github.com/user-attachments/assets/c4fa4ef4-2742-4958-a364-fe10289aba63)

## Levantar otro cluster con un runtime distinto.
```
minikube start -p cluster3 --container-runtime=cri-o
```
![image](https://github.com/user-attachments/assets/811f2dea-f90f-4d0f-af5b-0ad4ab21b83e)

## Borrar los cluster creados.
```
minikube delete -p clusterDesa
minikube delete -p cluster3
```
![image](https://github.com/user-attachments/assets/64f37501-eb15-454f-81e8-8c9a21b9a01b)
