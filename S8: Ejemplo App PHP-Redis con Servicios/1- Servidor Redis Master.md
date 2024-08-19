# Redis Master
## yaml del Redis junto con su servicio.
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: redis-master
spec:
  selector:
    matchLabels:
      app: redis
      role: master
      tier: backend
  replicas: 1
  template:
    metadata:
      labels:
        app: redis
        role: master
        tier: backend
    spec:
      containers:
      - name: master
        image: redis
        ports:
        - containerPort: 6379
---

#############
# SERVICIO  
#############
apiVersion: v1
kind: Service
metadata:
  name: redis-master-svc
  labels:
    app: redis
    role: master
    tier: backend
spec:
  ports:
  - port: 6379
    targetPort: 6379
  selector:
    app: redis
    role: master
    tier: backend
```
