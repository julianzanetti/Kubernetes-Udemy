# Labels.
### Vamos a realizar un ejemplo para visualizar nuestras etiquetas en un determinado objeto.
## Creamos nuestro manifest.
```
apiVersion: v1
kind: Pod
metadata:
  name: tomcat
  labels:
    estado: "desarrollo"
spec:
  containers:
  - name: tomcat
    image: tomcat
```
![image](https://github.com/user-attachments/assets/cc955953-6b92-4f35-a87e-25aa04ce5ef2)

## Creamos nuestro pod.
```
kubectl apply -f tomcat.yml
kubectl get pods
```
![image](https://github.com/user-attachments/assets/2fecc4dd-1ccf-4d73-a66d-0a0fbfbf0e38)

## Visualizar solamente las labels del pod.
```
kubectl get pod tomcat --show-labels
```
![image](https://github.com/user-attachments/assets/63d9f9df-dfa3-450c-a57f-245ae1cb17d1)

## Otra forma de visualizar las labels.
```
kubectl get pod tomcat -L nombre_etiqueta
```
![image](https://github.com/user-attachments/assets/55ba9583-59ac-4a97-a815-c2b7deb82307)

## Vamos a agregar otra label a nuestro objeto.
```
kubectl label objeto nombre_objeto id-label=valor
```
![image](https://github.com/user-attachments/assets/52978aee-8936-4779-9198-4e14411c3e7e)

## Modificar una label ya existente.
```
kubectl label objeto nombre_objeto --overwrite id-label=valor
```
![image](https://github.com/user-attachments/assets/bbd6e28c-e042-406d-a9cd-16565ccc01d3)

## Eliminar una etiqueta.
```
kubectl label objeto nombre_objeto id-label-
```
![image](https://github.com/user-attachments/assets/f19d3e7a-ec0c-4239-9fdc-ecbc04ab5f85)

## Realizar todo lo anterior pero en el yaml.
### Agregar label:
![image](https://github.com/user-attachments/assets/773e99cf-b00e-41c5-ba2d-a7680619a9fe)
![image](https://github.com/user-attachments/assets/cf532657-7a8b-43cd-ae70-2462094e12eb)

### Modificar label:
![image](https://github.com/user-attachments/assets/f171e365-136a-43be-a768-5af34e13c04b)
![image](https://github.com/user-attachments/assets/f14162e9-5fa9-4706-a107-7f6b769e01a3)

### Eliminar label:
![image](https://github.com/user-attachments/assets/435bb0d8-6006-43c3-a5c6-41676c9c6035)
![image](https://github.com/user-attachments/assets/e90518a0-0e38-4728-accd-311ac0893b0f)

## Visualizar labels en el Dashboard.
![image](https://github.com/user-attachments/assets/95be2471-234d-4059-b3f7-763f32e0fd97)
