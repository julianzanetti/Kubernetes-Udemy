# Node Selector en Deploy.
## Ejemplo de uso del NodeSelector en un deploy
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-d
spec:
  selector:   
    matchLabels:
      app: nginx
  replicas: 2
  template:  
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.7.9
        ports:
        - containerPort: 80
      nodeSelector: 
        aplicacion: web
```

> [!IMPORTANT]
> Recordar que los Nodos tienen que contener la etiqueta que nosotros ingresemos, asi matchea con ellos.
