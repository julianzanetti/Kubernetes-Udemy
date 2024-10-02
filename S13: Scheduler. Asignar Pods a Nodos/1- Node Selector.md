# Node Selector.
## Un ejemplo de archivo de configuracion con Node Selector.
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
     image: apasoft/nginx:v1
  nodeSelector:
    entorno: desarrollo
```

## Buscamos las etiquetas de nuestros nodos.
```
kubectl get nodes --show-labels
```
![image](https://github.com/user-attachments/assets/febdef4b-2d28-46db-a575-9a3913de7c19)

## Agregar una label a un Nodo.
```
kubectl label nodo ip-nodo clave=valor
```
![image](https://github.com/user-attachments/assets/d8da79fa-20b0-4ca0-a23d-1384a04222d3)
