# Escalar un Deployment.
## Aumentar el numero de replicas.
```
kubectl scale deploy nombre_deploy --replicas
```
![image](https://github.com/user-attachments/assets/6ab918bd-77a9-4fc5-bb43-686bff5b1136)

## Disminuir el numero de replicas.
```
kubectl scale deploy nombre_deploy --replicas
```
![image](https://github.com/user-attachments/assets/82836960-e1d7-4d8c-a7df-268e5a787fe6)

## Aumentar/disminuir las replicas de un deploy segun su label.
```
kubectl scale deploy nombre_deploy -l id-label=valor --replicas
```
![image](https://github.com/user-attachments/assets/d004abd3-c6fb-48f9-9a00-3e29fc88d005)
