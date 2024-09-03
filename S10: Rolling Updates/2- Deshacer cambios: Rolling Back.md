# Deshacer cambios: Rolling Back.
## Visualizar la version de la imagen de nuestro deploy.
```
kubectl describe deploy nginx-d | grep Image
```
![image](https://github.com/user-attachments/assets/0468ce60-5b28-43da-b8a9-366eaed9cad2)

## Vamos a volver a la primera version.
```
kubectl rollout history deploy nginx-d --revision=1 | grep Image
kubectl rollout undo deploy nginx-d  --to-revision=1
```
![image](https://github.com/user-attachments/assets/98a27a92-afc0-4be5-a51d-a277342cf574)

## Visualizar nuevamente la version de nuestro deploy.
```
kubectl describe deploy nginx-d | grep Image
```
![image](https://github.com/user-attachments/assets/829ec865-3f9f-4c25-bf6a-74080b39798a)

## Ver el historial de versiones.
```
kubectl rollout history deploy nginx-d
```
![image](https://github.com/user-attachments/assets/a7b7c310-e4d6-413d-b54b-356acdcf6b67)
