# Taint y Tolerations.
- ### Un Taint permite que un nodo no acepté uno o varios PODS
- ### Es por tanto lo contrario al Node Affinity
- ### Los Taints se aplican a los nodos y las tolerations a los PODS
- ### Los Taints pueden ser:
  - NoSchedule       --- No permite poner el POD en este nodo.
  - PreferNoSchedule --- Solo para el POD en este nodo si no se cumplen las otras condiciones.
  - NoExecute        --- Si el POD ya se encuentra en el nodo lo saca.
 
## Ejemplo de uso de los Taint y Tolerations.
### Asignamos a un POD que no sea utilizado por los PODS normales
```
kubectl taint nodes ip-nodo memoria=grande:NoSchedule
```
![image](https://github.com/user-attachments/assets/eb614d2d-79eb-4fe1-8b09-7a88b0110a5f)

> [!NOTE]
> Si ahora lanzaramos algun POD simple (con x replicas y una imagen), ninguno de estos pararia en el NODO con el Taint que especificamos antes.

### Deploy con Tolerancia al nodo con taint.
```
apiVersion: apps/v1 
kind: Deployment
metadata:
  name: nginx-d
spec:
  selector:   
    matchLabels:
      app: nginx
  replicas: 10
  template: 
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx
        ports:
        - containerPort: 80
      tolerations:
      - effect: NoSchedule
        key: memoria
        operator: Equal
        value: grande
```
> [!NOTE]
> De esta forma algun POD parara en el NODO con el tag memoria=grande.
