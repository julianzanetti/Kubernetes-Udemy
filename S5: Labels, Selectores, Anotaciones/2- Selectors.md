# Selectors.
## Creamos varios manifest con distintas labels.
```
apiVersion: v1
kind: Pod
metadata:
  name: tomcat1
  labels:
    estado: "produccion"
    responsable: "julian"
spec:
  containers:
  - name: tomcat
    image: tomcat
```
![image](https://github.com/user-attachments/assets/5490cd84-4bc3-4288-ac05-f77fa2bcfd7e)
![image](https://github.com/user-attachments/assets/346efb6d-650b-4d03-bf95-3d2e63e85608)

## Visualizar solamente los POD con estado=desarrollo.
```
kubectl get pods --show-labels -l estado=desarrollo
```
![image](https://github.com/user-attachments/assets/4e501abf-77b1-40c8-bd90-b7cf4020d40c)

## Visualizar solamente los POD con responsable=julian
```
kubectl get pods --show-labels -l responsable=julian
```
![image](https://github.com/user-attachments/assets/a9b387b8-c258-4c79-8823-acc6a21823c2)

## Visualizar solamente los POD con responsable=julian y estado=produccion.
```
kubectl get pods --show-labels -l responsable=julian,estado=produccion
```
![image](https://github.com/user-attachments/assets/72261b83-e317-46fd-b4cf-a94019f7ded5)

## Visualizar solamente los POD en el cual responsable no sea julian.
```
kubectl get pods --show-labels -l responsable!=julian
```
![image](https://github.com/user-attachments/assets/94a661bf-c178-47f3-a031-0fcbe692fdd6)

## Visualizar los POD en desarrollo y testing.
```
kubectl get pods --show-labels -l 'estado in (desarrollo,testing)'
```
![image](https://github.com/user-attachments/assets/f914e900-b969-4ae4-8a60-7c5b920e265d)

## Borrar todos los PODS de produccion y testing.
```
kubectl delete pods -l 'estado in (produccion,testing)'
```
![image](https://github.com/user-attachments/assets/476c1db9-df75-4b86-bcf7-759c0b1c860c)
