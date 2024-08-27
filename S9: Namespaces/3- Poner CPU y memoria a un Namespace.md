# Limitar Namespace.
## Limitamos nuestro namespace de forma declarativa.
```
apiVersion: v1
kind: LimitRange
metadata:
  name: recursos
spec:
  limits:
  - default:
      memory: 512Mi
      cpu: 1
    defaultRequest:
      memory: 256Mi
      cpu: 0.5
    max:
      memory: 1Gi
      cpu: 4
    min:
      memory: 128Mi
      cpu: 0.5
    type: Container
```
```
kubectl apply -f limites.yaml -n dev1
```
![image](https://github.com/user-attachments/assets/74757bf0-944d-4f27-91b1-e4bbbe86b6eb)

## Describimos nuestro namespace.
```
kubectl describe namespace dev1
```
![image](https://github.com/user-attachments/assets/4633f949-7514-4b24-8e16-a5172d5fe245)
