# Rolling Updates. Modificar una aplicacion.
## Creamos un deployment de nginx con una version especifica.
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-d
  labels:
    estado: "1"
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 10
  strategy:
    type: RollingUpdate
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.26
        ports:
        - containerPort: 80
```
```
kubectl apply -f nginx.yaml
kubectl get pods
kubectl describe deploy nginx | grep Image
```
![image](https://github.com/user-attachments/assets/ac128acc-36ec-4c19-b8fc-fbdee2be6685)

## Ver el historial del deploy.
```
kubectl rollout history deploy nginx-d
```
![image](https://github.com/user-attachments/assets/c470e88e-3aed-49a7-b325-c3c8ad7d4b11)

## Vamos a actualizar a la ultima version del nginx.
![image](https://github.com/user-attachments/assets/b4e7e1e2-2952-414b-b2d0-12c4d73ab896)

```
kubectl apply -f nginx.yaml
```
![image](https://github.com/user-attachments/assets/d291f894-b554-4615-9155-aeeb8d484290)
### Si prestamos atencion podemos notar que el hash de los pods antiguos y los nuevos cambian.

## Consultamos nuevamente el historial.
```
kubectl rollout history deploy nginx-d
```
![image](https://github.com/user-attachments/assets/c805c797-1abb-4fec-b29f-94b0d90ee540)

## Comparamos la revision 1 y 2.
```
kubectl rollout history deploy nginx-d --revision=1
kubectl rollout history deploy nginx-d --revision=2
```
![image](https://github.com/user-attachments/assets/7c8d5a5c-19ec-492d-9e7f-1d1a9179ce89)

## Consultar los replicaset.
```
kubectl get rs
```
![image](https://github.com/user-attachments/assets/b85cf684-8c6c-4355-9a50-9b4bf0ed21c2)

## Agregamos un servicio a nuestro manifest y cambiamos nuevamente la version de la imagen.
```
apiVersion: v1
kind: Service
metadata:
  name: nginx-svc
  labels:
    app: nginx
spec:
  selector:
    app: nginx
  type: NodePort
  ports:
  - port: 80
    nodePort: 31000
    protocol: TCP
```
![image](https://github.com/user-attachments/assets/f1854df7-4a6d-47ec-b25b-efbe8bd0b5d0)
![image](https://github.com/user-attachments/assets/07730068-58ad-44de-8713-eb81efa331c9)
![image](https://github.com/user-attachments/assets/0791d266-5527-49dd-9fcc-16be10ebde10)
![image](https://github.com/user-attachments/assets/cb782551-394a-4ae3-ac3a-3da4b670542e)
