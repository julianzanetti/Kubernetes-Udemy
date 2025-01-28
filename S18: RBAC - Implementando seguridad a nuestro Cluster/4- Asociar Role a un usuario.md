# Asociar Role a un usuario.
## Creamos un POD en nuestro ns creado anteriormente.
```
kubectl run nginx --image=nginx -n ventas
```
![image](https://github.com/user-attachments/assets/53a69657-06ac-4da0-b629-3432bd55e681)

## Vemos los roles que tenemos en nuestro namespace.
```
kubectl get roles -n ventas
```
![image](https://github.com/user-attachments/assets/71a96930-4e41-4f10-aaa7-bab67fb32d86)

## Asignamos el role al usuario desa1.
```
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
   name: role-operador
   namespace: ventas
subjects:
- kind: User
  name: desa1 
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role 
  name: operador 
  apiGroup: rbac.authorization.k8s.io
```
![image](https://github.com/user-attachments/assets/3818ac60-c648-4390-8840-041f6e1d3b9e)

## Probamos visualizar el POD.
![image](https://github.com/user-attachments/assets/30c74290-60b4-44fd-b9d2-343c56e6edcd)

## Tratemos de crear otro POD.
```
kubectl --kubeconfig=/home/Kubernetes/RBAC/certs/.kube/config run nginx1 --image=nginx -n ventas
```
![image](https://github.com/user-attachments/assets/54b707ac-a626-499a-a492-b69bee290902)
> [!NOTE]
> UsNo deja crear porque como vimos anteriormente el ROL solamente permite (get watch list) y no create.
