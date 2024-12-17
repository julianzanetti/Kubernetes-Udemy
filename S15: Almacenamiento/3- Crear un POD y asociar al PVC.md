# Crear un POD y asociar al PVC.
## Archivo de configuracion del POD.
```
apiVersion: v1
kind: Pod
metadata:
  name: pv-pod
spec:
  volumes:
    - name: pv-storage
      persistentVolumeClaim:
        claimName: pv-claim
  containers:
    - name: task-pv-container
      image: nginx
      ports:
        - containerPort: 80
          name: "http-server"
      volumeMounts:
        - mountPath: "/var/www/html/"
          name: pv-storage
```
- volumes/name: Nombre del volumen del POD.
- claimName: Indicar el PVC al que queremos asociar.
- volumeMounts: Ruta donde guardamos en el POD y nombre del volumen.
![image](https://github.com/user-attachments/assets/d30906c1-55f5-4bac-8491-83815bd88448)

## Ingresamos al nodo donde fue el POD.
```
minikube ssh -p nombre-cluster -n nombre-nodo
```
![image](https://github.com/user-attachments/assets/8ce9e0c0-6ee4-4288-be32-e1d698bdae6e)
![image](https://github.com/user-attachments/assets/956d726f-a11a-4809-a513-1b9a846c04c9)

## Verificamos que se haya creado el directorio indicado en el PV.
![image](https://github.com/user-attachments/assets/07bf86d8-9a1c-49f3-a495-c42695b0d9e9)
![image](https://github.com/user-attachments/assets/9771082e-6d6e-401a-9e01-a545de656efd)
### Ejemplo en el nodo 03 no existe ningun archivo.
![image](https://github.com/user-attachments/assets/6a8b9b79-24f9-4228-816f-c9c5b8a88dd5)
