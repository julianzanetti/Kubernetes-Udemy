# Endpoints.
## Ver los endpoint asociados al servicio.
```
kubectl get svc
kubectl describe svc web-svc
```
![image](https://github.com/user-attachments/assets/48f7ae24-00c8-4e71-9897-a9db5433a117)

## Ver y describir todos los endpoints.
```
kubectl get endpoints
kubectl describe endpoints web-svc
```
![image](https://github.com/user-attachments/assets/bd57500c-af07-4bba-b626-6c776dacc090)

## Visualizar el endpoint en formato yaml.
```
kubectl get endpoints web-svc -o yaml
```
![image](https://github.com/user-attachments/assets/30d5a3a2-b7a0-4de4-9cbd-ffeb7644efde)
