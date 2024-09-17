# Secret de forma Declarativa.
## Creamos un secret con los valores ya encriptados.
```
echo -n "usu1" | base64
echo -n "password-usu1" | base64
```
```
apiVersion: v1
kind: Secret
metadata:
  name: secreto1
type: Opaque
data:
  usuario1: dXN1MQ==
  usu1-pass: cGFzc3dvcmQtdXN1MQ==
```

## Creamos un segundo secret con los valores en string.
```
apiVersion: v1
kind: Secret
metadata:
  name: secreto2
type: Opaque
stringData:
  usuario2: 'usu2'
  usu2-pass: 'password-usu2'
```

## Creamos un POD y le pasamos como parameto los dos secrets.
```
apiVersion: v1
kind: Pod
metadata:
  name: pod1
spec:
  containers:
    - name: test-container
      image: ubuntu
      command: [ "/bin/sh", "-c", "sleep 1000000" ]
      envFrom:
        - secretRef:
              name: secreto1
        - secretRef:
              name: secreto2
  restartPolicy: Never
```

## Ingresamos al POD y consultamos las variables.
```
kubectl exec -it pod1 bash 
```
![image](https://github.com/user-attachments/assets/187d0d99-1c23-496f-a09d-002ba221d012)
