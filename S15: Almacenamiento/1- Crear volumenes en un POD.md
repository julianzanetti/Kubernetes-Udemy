# Crear volumenes en un POD
## Ejemplo de un archivo de configuracion con los diferentes tipos de volumenes.
```
apiVersion: v1
kind: Pod
metadata:
  name: volumenes
spec:
  containers:
  - name: nginx
    image: nginx
    volumeMounts:
    - mountPath: /home
      name: home
    - mountPath: /git
      name: git
      readOnly: true
    - mountPath: /temp
      name: temp
  volumes:
  - name: home
    hostPath:
      path: /home/kubernetes/datos
  - name: git
    gitRepo:
      repository: https://github.com/apasoftTraining/cursoKubernetes.git
  - name: temp
    emptyDir: {}
```
![image](https://github.com/user-attachments/assets/09f1959d-17c8-4df9-93bd-529b202a75e5)

## Ingresamos a nuestro nodo de Minikube y verificamos que se haya creado el /datos.
```
minikube ssh
```
![image](https://github.com/user-attachments/assets/7b759747-86d9-4e93-8141-6c83a90fd376)

## Crear un archivo y verificar que en el POD se haya creado.
```
touch prueba
```
![image](https://github.com/user-attachments/assets/8251e889-f72f-4ac4-881a-4d1d4abe403b)
![image](https://github.com/user-attachments/assets/4174d5ff-1f21-4cce-969d-15406d75720f)

## Realizar el mismo paso desde el POD y verificar en el NODO.
![image](https://github.com/user-attachments/assets/423e7eea-ec93-4282-ac9b-d35ac5d1a0ea)
![image](https://github.com/user-attachments/assets/d088f194-7811-451a-8a2e-544741e3673f)
