# Ejemplo: Wordpress con Mysql.
## Preparacion del entorno.
### Utilizaremos un un master y dos esclavos:
![image](https://github.com/user-attachments/assets/9134c8f7-d781-49ba-904d-718b4077c8af)

### Crearemos un workdir con dos directorios (esto se realiza en el master y en los dos esclavos):
```
mkdir /home/kubernetes/datos/mysql
mkdir /home/kubernetes/datos/wordpress
```
![image](https://github.com/user-attachments/assets/ed1aa37e-15f6-49d6-88bc-6ad10626b457)

### Configuramos los permisos de NFS para los dos directorios en el /etc/exports.
![image](https://github.com/user-attachments/assets/d744babc-b75e-43b8-a6be-1ae145e56347)

### Rebotamos el kernel.
```
systemctl restart nfs-kernel-server
```
![image](https://github.com/user-attachments/assets/8eb6ec03-c34d-4369-9f98-f79932079797)

### Montamos en los esclavos los workdir del master.
```
mount -t nfs ip-master:/home/kubernetes/datos/mysql /home/kubernetes/datos/mysql
mount -t nfs ip-master:/home/kubernetes/datos/wordpress /home/kubernetes/datos/wordpress
```
![image](https://github.com/user-attachments/assets/00e87b3f-7be3-4610-be05-2bff9fd73361)

## Crear el PV y PVC.
