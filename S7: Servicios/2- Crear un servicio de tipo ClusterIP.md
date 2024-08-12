# Crear un servicio de tipo ClusterIP.
## Vamos a crear un servicio de sql-host y otro de sql-cliente.
```
kubectl create deployment mysql-host --image=mysql
kubectl create deployment mysql-cliente --image=mysql --command -- sh -c "sleep infinity"
```
![image](https://github.com/user-attachments/assets/8820666b-33c1-48b1-9194-e6833850ae58)

## Agregamos las variables de entorno mysql al deploy.
```
kubectl set env deployment/mysql-host MYSQL_ROOT_PASSWORD=password
```
![image](https://github.com/user-attachments/assets/427fa7a2-963d-42aa-806f-29080f6fe630)

## Exponemos el deploy del mysql-host.
```
kubectl expose deployment mysql-host --port=3306 --type=ClusterIP
```
![image](https://github.com/user-attachments/assets/0fa3862e-b089-4f03-8196-92a1c2631976)

## Ingresamos al mysql-host y creamos una db.
```
kubectl exec -it mysql-host -- bash
mysql -u root -p
create databases mibasededatos;
```
![image](https://github.com/user-attachments/assets/d44723c8-1b28-4a2c-a653-702ee8810d13)
![image](https://github.com/user-attachments/assets/598a2caf-e830-4773-9dd5-95334d674088)

## Ingresar al mysql-client y de ahi ir al mysql-host.
```
kubectl exec -it mysql-cliente -- bash
mysql -h mysql-host -u root -p
show databases;
```
![image](https://github.com/user-attachments/assets/1aacb1bc-9b0f-4a44-95eb-e1a797955cb5)
