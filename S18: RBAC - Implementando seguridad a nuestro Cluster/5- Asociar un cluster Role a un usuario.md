# Asociar un cluster Role a un usuario.
## Recordar que nuestro usuario no puede crear pods.
![image](https://github.com/user-attachments/assets/52c7f6be-7e2c-46c2-afa4-b588060b3f73)

## Recordar que hemos creado un clusterrole llamado desarrollo.
![image](https://github.com/user-attachments/assets/1e6de160-696f-4965-aa32-958859b1a752)
> [!NOTE]
> Vemos que el recurso PODS tiene permiso para crear.

## Vamos a asignar nuestro clusterrole a nuestro usuario desa1.
```
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
   name: cluster-role-ejemplo
subjects:
- kind: User
  name: desa1 
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: ClusterRole
  name: desarrollo
  apiGroup: rbac.authorization.k8s.io
```
![image](https://github.com/user-attachments/assets/ad0f112d-08e3-46b7-a0cf-5e2e45a6cf4f)

## Tratamos de crear un POD.
```
kubectl --kubeconfig=/home/Kubernetes/RBAC/certs/.kube/config run nginx1 --image=nginx -n ventas
kubectl --kubeconfig=/home/Kubernetes/RBAC/certs/.kube/config get pods -n ventas
```
![image](https://github.com/user-attachments/assets/52bb594b-eb71-459c-9e73-bbfa96f122cc)
