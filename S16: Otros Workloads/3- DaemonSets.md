# DaemonSets.
### Crea un POD por cada nodo que tengamos en nuestro cluster.
## Ejemplo de Uso.
### Verificamos nuestra cantidad de nodos.
```
kubectl get nodes
```
![image](https://github.com/user-attachments/assets/6827bc0c-b4c0-41bf-b642-5eaf869defcb)

### Ejecutamos nuestro archivo de tipo DaemonSet.
```
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: log-daemonset
spec:
  selector:
    matchLabels:
      name: log 
  template:
    metadata:
      labels:
        name: log
    spec:
      containers:
      - name: log
        image: logstash:8.4.1
```
![image](https://github.com/user-attachments/assets/e5a7db5a-18b1-4657-9a8f-5d5df9eb846c)

### Verificamos que los PODS se haya creado en todos los nodos.
```
kubectl get pods -o wide
```
![image](https://github.com/user-attachments/assets/ef39b640-7005-4e65-9728-7ebd1d964c45)

### Que pasa si agregamos otro nodo.
```
kubectl get nodes
```
![image](https://github.com/user-attachments/assets/05fe43ea-8a34-467f-bc6c-5f3844fb59f9)

```
kubectl get pods -o wide
```
![image](https://github.com/user-attachments/assets/412ffd0b-af53-4d02-84ee-974e592b7dcb)
