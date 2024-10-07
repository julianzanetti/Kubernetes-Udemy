# Limitar los recursos de los contenedores en una NameSpace.
## Ejemplo de configuracion de un LimitRange.
```
apiVersion: v1
kind: LimitRange
metadata:
  name: recursos
spec:
  limits:
  - default:
      memory: 512Mi
      cpu: "1"
    defaultRequest:
      memory: 256Mi
      cpu: "0.5"
    max:
      memory: 1Gi
      cpu: "4"
    min:
      memory: 128Mi
      cpu: "0.5"
    type: Container
```
```
kubectl apply -f limites.yaml
kubectl describe ns default
```
![image](https://github.com/user-attachments/assets/a56b0673-c0d7-40c9-bd8e-03d05cb3b42f)
