# Fichero kubeconfig.
## Ruta donde se aloja el fichero.
![image](https://github.com/user-attachments/assets/c945fbbb-df6d-4384-9502-7f5fac715b2a)
![image](https://github.com/user-attachments/assets/5985316d-74fc-44ef-a8f7-f8aa6eb025ce)

## Comando para ver el mismo archivo.
```
kubectl config view
```
![image](https://github.com/user-attachments/assets/92a51ae2-d069-4708-97a8-21a19192b888)

## Agregar un nuevo cluster.
```
kubectl config set-cluster nombre_cluster --server=direccion
```
![image](https://github.com/user-attachments/assets/dcfb2047-25a8-436f-95fd-21b02cb8e470)

## Agregar usuarios y credenciales.
```
kubectl config set-credentials nombre_usu --username=admin --password=secret
```
![image](https://github.com/user-attachments/assets/728d07fa-b7f1-4089-ac21-fb0230636b3d)
