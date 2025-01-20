# Sonda Liveness de tipo HTTP.
## Ejemplo de uso.
- ### Deploy:
```
apiVersion: apps/v1 # i se Usa apps/v1beta2 para versiones anteriores a 1.9.0
kind: Deployment
metadata:
  name: web-d
spec:
  selector:   #permite seleccionar un conjunto de objetos que cumplan las condicione
    matchLabels:
      app: web
  replicas: 1 # indica al controlador que ejecute 1 pods
  template:   # Plantilla que define los containers
    metadata:
      labels:
        app: web
    spec:
      containers:
      - name: web-d-777b977ff9
        image: apasoft/sonda-web:latest
        ports:
        - containerPort: 80
        livenessProbe:
            httpGet:
                path: /sonda.html
                port: 80
            initialDelaySeconds: 3
            periodSeconds: 3
```

- ### Servicio:
```
apiVersion: v1
kind: Service
metadata:
  name: web-svc
  labels:
     app: web
spec:
  type: NodePort
  ports:
  - port: 80
    nodePort: 30002
    protocol: TCP
  selector:
     app: web
```
![image](https://github.com/user-attachments/assets/d34bfd58-3600-4952-ae15-ea333c99c94c)
![image](https://github.com/user-attachments/assets/fa9c8c54-e3a4-4f92-b825-9dc8d1d89815)
![image](https://github.com/user-attachments/assets/e9ed0caa-6c3c-4225-a0ff-662b49728380)

## Fallo de la sonda.
- ### Eliminamos el archivo sonda.html dentro del contenedor.
![image](https://github.com/user-attachments/assets/104b4be1-50c0-481c-bb60-9a223686feff)

- ### Verificamos el estado del POD.
```
kubectl describe pod ID
kubectl get pods -o wide
```
![image](https://github.com/user-attachments/assets/cf20c729-86fd-4c46-87f2-d65d96e6e5c6)
![image](https://github.com/user-attachments/assets/1fdce2f8-7ffb-43be-bed2-bd049f4a0952)

> [!IMPORTANT]
> Vemos que elimino el contenedor y volvio a reconstruirlo.
