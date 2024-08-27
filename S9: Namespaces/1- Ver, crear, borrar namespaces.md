# Ver, Crear, Borrar y Establecer namespaces.
## Ver nuestros namespaces.
```
kubectl get namespaces
```
![image](https://github.com/user-attachments/assets/6e0e7192-7035-40ff-bf55-03998002f68d)

## Ver los PODS de un namespaces.
```
kubectl get pods -n nombre_namespaces
```
![image](https://github.com/user-attachments/assets/0061ccf2-2d76-45d1-85e0-3b371b7726dc)

## Crear un namespaces.
### - Forma imperativa:
```
kubectl create namespace n1
```
![image](https://github.com/user-attachments/assets/5f077f97-656b-463d-ac84-96f0279e188c)

### - Declarativa:
```
apiVersion: v1
kind: Namespace
metadata:
  name: dev1
  labels:
     tipo: desarrollo
```
![image](https://github.com/user-attachments/assets/e7b959e2-6515-4476-85d4-717b908f859c)

```
kubectl apply -f
kubectl describe namespaces dev1
```
![image](https://github.com/user-attachments/assets/fbbfec27-fcda-47d7-8a5d-9529d71f16f7)
![image](https://github.com/user-attachments/assets/b8a34e1f-db4e-47f0-99f8-2136a1822fc3)

## Borrar un namespaces.
```
kubectl delete namespaces n1
```
![image](https://github.com/user-attachments/assets/49243f9f-2661-42be-bb7c-4f014a4e8bd4)

## Establecer una namespaces por defecto.
```
kubectl config set-context --current --namespace=nombre_namespaces
```
![image](https://github.com/user-attachments/assets/49e3656c-2280-47a6-94d2-b49be983fee9)

```
kubectl config view
```
![image](https://github.com/user-attachments/assets/33ad96d2-34aa-4a32-b713-7a2a0f85694f)

