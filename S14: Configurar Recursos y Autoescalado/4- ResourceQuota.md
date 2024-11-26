# ResourceQuota - Limitar los recursos de una Namespace.
## Ejemplo de un Resource.yaml
```
apiVersion: v1
kind: ResourceQuota
metadata:
  name: pods-grandes
spec:
  hard:
    cpu: "100"
    memory: "500Mi"
    pods: "5"
```
![image](https://github.com/user-attachments/assets/ab9bbef2-f48b-4777-b249-8c0703cdcda6)

## Se divide por limits y requests.
```
apiVersion: v1
kind: ResourceQuota
metadata:
  name: pods-grandes
spec:
  hard:
    requests.cpu: "100"
    requests.memory: 500Mi
    limits.cpu: "500"
    limits.memory: 1Gi
    pods: "5"
```
![image](https://github.com/user-attachments/assets/0390e5e1-f752-474a-8282-e1bf0fafcaaf)

## Levantamos un POD.
```
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    zone: prod
    version: v1
spec:
  containers:
   - name: nginx   
     image: nginx
     resources:
      limits:
        memory: "200Mi"
        cpu: "1"
      requests:
        memory: "150Mi"
        cpu: "0.5"
```
![image](https://github.com/user-attachments/assets/49aa8c1c-1115-4380-816e-b98892d0f09b)

## Que pasa si sobrepasamos tanto el requests como el limits.
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-d
  labels:
    estado: "1"
spec:
  selector:   #permite seleccionar un conjunto de objetos que cumplan las condicione
    matchLabels:
      app: nginx
  replicas: 2 # indica al controlador que ejecute 2 pods
  template:   # Plantilla que define los containers
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx
        ports:
        - containerPort: 80
        resources:
          limits:
              memory: "400Mi"
              cpu: "1"
          requests:
              memory: "256Mi" 
              cpu: "0.5"

```
![image](https://github.com/user-attachments/assets/bd06a4f3-48af-4bb9-996c-0e89e688e51e)

### Vemos que solamente a creado una replica de las dos requeridas, porque hemos sobrepasado el limite establecido.
![image](https://github.com/user-attachments/assets/9ebede51-c075-4a85-aaa0-a3ca0dc1e699)

## Que pasa si aumentamos el limite.
```
apiVersion: v1
kind: ResourceQuota
metadata:
  name: pods-grandes
spec:
  hard:
    requests.cpu: "100"
    requests.memory: 1Gi
    limits.cpu: "500"
    limits.memory: 1Gi
    pods: "5"
```
![image](https://github.com/user-attachments/assets/93abae4c-c228-4945-baee-e687c4368dec)
