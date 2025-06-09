# PODS Multicontenedores.
## Creamos un Pod que contiene dos contenedores.
- En este caso el primer contenedor tiene una imagen nginx que escucha por el puerto 80.
- El segundo contenedor es un alpine que hace un ping c/ 10 segundos a nuestro POD.
```
apiVersion: v1
kind: Pod
metadata:
  name: multi
spec:
  containers:
  - name: web
    image: nginx
    ports:
    - containerPort: 80  
  - name: frontal
    image: alpine
    command: ["watch", "-n10", "ping",  "localhost"]
```
![image](https://github.com/user-attachments/assets/df01abeb-9975-43c6-bec8-7addca2377e6)

```
kubectl apply -f nombre_pod
kubectl get pods
```
![image](https://github.com/user-attachments/assets/2b32cf93-9df0-49a7-b3ff-6d98081cb847)
![image](https://github.com/user-attachments/assets/2f08069c-316f-49c4-8206-ca7c527efe0f)

## Verificamos que efectivamente haya creado dos contenedores.
```
kubectl describe pod nombre_pod
```
![image](https://github.com/user-attachments/assets/f9725ce3-7450-4f05-ae26-ff38866ebcca)

## Ver el log del contenedor frontal.
```
kubectl logs --tail 10 nombre_pod -c frontal
```
![image](https://github.com/user-attachments/assets/53308ffd-c9ec-4f88-b1ee-558b9ee88df9)
