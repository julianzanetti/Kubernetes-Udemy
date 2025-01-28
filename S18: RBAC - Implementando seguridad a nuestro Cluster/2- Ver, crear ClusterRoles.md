# Ver, crear ClusterRoles - Permisos a nivel Cluster.
## Ver los clusterRoles.
```
kubectl get clusterrole
```
![image](https://github.com/user-attachments/assets/f59ab50e-f3d6-4956-bdd9-bfb1f08a0d91)

## Crear clusterRole.
```
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: desarrollo
rules:
- apiGroups: [""]
  resources: ["secrets","configmaps"]
  verbs: ["get", "watch", "list"]
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["create", "watch", "list","get","edit"]
```
![image](https://github.com/user-attachments/assets/37aca132-2492-4c77-beb0-f784f613845f)
![image](https://github.com/user-attachments/assets/b7cf80c2-c556-46d9-a8aa-9f6516692508)
