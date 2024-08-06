# Crear un deployment en modo imperativo y ver su info.
## Vamos a crear nuestro primer deployment.
```
kubectl create deployment nombre_deploy --image=imagen
```
![image](https://github.com/user-attachments/assets/48697253-6c38-4ba3-a882-d7278577829a)

## Visualizar nuestro deploy.
```
kubectl get deploy
```
![image](https://github.com/user-attachments/assets/17130b46-1b69-42c0-84fb-125dc3fd4709)

## Visualizar el replicaset creado junto con el deployment.
```
kubectl get rs
```
![image](https://github.com/user-attachments/assets/f095b94b-4715-4e70-b76c-0b8fe11f3f1c)

## Visualizar los pods que creo el deployment.
```
kubectl get pods
```
![image](https://github.com/user-attachments/assets/b635a68b-04b1-4e58-aa0a-d26e36ab5a11)

## Vamos a ver la info que tiene nuestro deploy.
```
kubectl describe deploy nombre_deploy
```
![image](https://github.com/user-attachments/assets/3eaeb845-6ec8-49a9-bf1f-a7cbd8dbd975)

## Visualizar la salida en formato yaml.
```
kubectl get deploy nombre_deploy -o yaml
```
![image](https://github.com/user-attachments/assets/4dd85c0c-1d4e-4918-aad8-c19a22c70eab)
