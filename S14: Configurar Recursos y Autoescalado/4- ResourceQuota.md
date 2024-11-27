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

# Trabajar con multiples Quotas.
## Ejemplo de configuracion.
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
  scopeSelector:
    matchExpressions:
    - operator : In
      scopeName: PriorityClass
      values: ["produccion"]
---
apiVersion: v1
kind: ResourceQuota
metadata:
  name: pods-peques
spec:
  hard:
    requests.cpu: "50"
    requests.memory: 100Mi
    limits.cpu: "100"
    limits.memory: 200Mi
    pods: "10"
  scopeSelector:
    matchExpressions:
    - operator : In
      scopeName: PriorityClass
      values: ["desarrollo"]
```

> [!IMPORTANT]
> Para que las Multiples quotas funcionen recordar que si o si ya tiene que existir las PriorityClass [Clase siguiente].
> kubectl get pc

![image](https://github.com/user-attachments/assets/4ca23fb9-3317-49f0-bf50-18425fcb851e)
![image](https://github.com/user-attachments/assets/11874060-a7ba-405e-84f3-d9129ce869e3)


## Ejemplo de Pod asignado a una quota a traves del priorityclass.
```
apiVersion: v1
kind: Pod
metadata:
  name: nginx1
  labels:
    zone: prod
    version: v1
spec:
  containers:
   - name: nginx   
     image: apasoft/nginx:v1
     resources:
      limits:
        memory: "100Mi"
        cpu: "1"
      requests:
        memory: "10Mi"
        cpu: "0.5"
  priorityClassName: desarrollo
```
![image](https://github.com/user-attachments/assets/d881d6d8-a773-48ce-97a4-ab916cf135f6)
