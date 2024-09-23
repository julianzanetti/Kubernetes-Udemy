# Fichero kubeconfig.
## Ruta donde se aloja el fichero.
![image](https://github.com/user-attachments/assets/c945fbbb-df6d-4384-9502-7f5fac715b2a)
![image](https://github.com/user-attachments/assets/b620ecf1-d8ad-40e9-b667-42e7a11cab59)

## Comando para ver el mismo archivo.
```
kubectl config view
```
![image](https://github.com/user-attachments/assets/074e9e89-3042-4de9-9126-a831fd21bdca)

## Agregar un nuevo cluster.
```
kubectl config set-cluster nombre_cluster --server=direccion
```
![image](https://github.com/user-attachments/assets/d1d56abd-daf7-4ce8-8610-55d84473bbd3)

## Agregar usuarios y credenciales.
```
kubectl config set-credentials nombre_usu --username=admin --password=secret
```
![image](https://github.com/user-attachments/assets/728d07fa-b7f1-4089-ac21-fb0230636b3d)
