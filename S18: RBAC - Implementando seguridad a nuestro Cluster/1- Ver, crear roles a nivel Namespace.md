# Ver, crear roles a nivel Namespace.
## Creamos una ns.
```
kubectl create namespace ventas
```
![image](https://github.com/user-attachments/assets/0e6aa749-fec9-40cc-9642-c0eeadefa549)

## Creamos un Rol.
```
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: ventas
  name: operador
rules:
- apiGroups: [""] 
  resources: ["pods"]
  verbs: ["get", "watch", "list"]
```
> [!NOTE]
> name: Nombre del rol.
> apiGroups: Url de APIS para acceder a un recurso (kubectl get api-resources)
> resource: recurso que queremos gestionar con este rol
> verbs: operaciones que realiza sobre el recurso.

## Ver el Rol creado.
```
kubectl get roles -n ventas
```
![image](https://github.com/user-attachments/assets/5e4dddfe-e036-470b-88d7-5ddbdc250ede)
![image](https://github.com/user-attachments/assets/2ada3ce2-622a-47e7-b406-9e686f216709)
