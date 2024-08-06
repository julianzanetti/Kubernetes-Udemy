# Anotaciones.
## Crear el siguiente manifest.
```
apiVersion: v1
kind: Pod
metadata:
  name: tomcat4
  labels:
    estado: "produccion"
    responsable: "julian"
  annotations:
    doc: "Se debe compilar con gcc"
    adjunto: "Ejemplo de anotacion"
spec:
  containers:
  - name: tomcat
    image: tomcat
```
![image](https://github.com/user-attachments/assets/8a702be0-d6cb-47d7-913c-ba0954690c34)
![image](https://github.com/user-attachments/assets/4308c0c7-0bdb-45c1-a868-bf2b029d8811)

## Visualizar nuestras anotaciones.
```
kubectl describe pod tomcat4
```
![image](https://github.com/user-attachments/assets/f9e7851f-3978-4c22-98d0-21996d376d57)

## Otra forma de visualizar.
```
kubectl get pod tomcat4 -o jsonpath={.metadata.annotations} | jq
```
![image](https://github.com/user-attachments/assets/3a6b02cc-1dcc-49b5-989a-faf7b32fd0ee)

Hay que tener instalado previamente jq

## Visualizar las anotaciones en el Dashboard.
![image](https://github.com/user-attachments/assets/829756f5-3e53-475f-8fd8-4ff293179f88)
