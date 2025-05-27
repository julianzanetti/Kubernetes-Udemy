# Secrets de tipo Docker.
## Creamos un secret con los datos de nuestro usuario al que vamos a ingresar al registro privado
- En este caso es mi usuario de docker hub y el registro se encuentra alojado ahi.
```
kubectl create secret docker-registry midocker --docker-server=docker.io --docker-username=user --docker-password=password --docker-email=mail
```

## Creamos un pod con la imagen que queremos descargar de nuestro registro privado, y vinculamos nuestro secret.
![image](https://github.com/user-attachments/assets/69b998b9-9975-4647-8aef-754cc4aa5d2d)
```
apiVersion: v1
kind: Pod
metadata:
  name: pod1
spec:
  containers:
  - name: pod1
    image: julianzanetti/kubernetes-web
  imagePullSecrets:
    - name: midocker
```
```
kubectl apply -f .
kubectl get pod
```
![image](https://github.com/user-attachments/assets/69a7170b-75de-40b5-be24-73921b10b778)

## Ver los eventos del pod.
```
kubectl describe pod pod1
```
![image](https://github.com/user-attachments/assets/7607dc83-fcba-469c-a6b7-712c5df6c138)
