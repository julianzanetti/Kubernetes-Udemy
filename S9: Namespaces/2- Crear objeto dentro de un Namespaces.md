# Crear objeto dentro de un Namespaces.
## Creamos un Deploy.
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: elastic
  labels:
    tipo: "desarrollo"
spec:
  selector:
    matchLabels:
      app: elastic
  replicas: 2
  strategy:
    type: RollingUpdate
  minReadySeconds: 2
  template:
    metadata:
      labels:
        app: elastic
    spec:
      containers:
      - name: elastic
        image: elasticsearch:7.6.0
        ports:
        - containerPort: 9200
```
![image](https://github.com/user-attachments/assets/fbe2970a-e05c-42c4-abb9-2e5004d89947)

```
kubectl apply -f elastic.yaml -n dev1
```
![image](https://github.com/user-attachments/assets/e606c7c2-9662-4024-a88a-1e1a8b3aa182)

## Ver si el deploy se creo dentro del namespaces indicado.
```
kubectl get deploy elastic -n dev1
```
![image](https://github.com/user-attachments/assets/9805effa-a25a-4027-abee-172e9e6bb484)

```
kubectl describe deploy elastic -n dev1 | grep Namespace
```
![image](https://github.com/user-attachments/assets/45e4b20d-2bf6-4a01-92d4-fcefccd66bf0)

```
kubectl get pods -n dev1
```
![image](https://github.com/user-attachments/assets/37a6d6ae-a55d-4e5b-9e38-9067fdfbbd53)
