# ConfigMaps y Volumenes.
## Creamos nuestro volumen de tipo cm y un pod que va a contener nuestro volumen.
### CM:
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: config-volumen
  namespace: default
data:
  ENTORNO: "desarrollo"
  VERSION: "1.0" 
```
### POD:
```
apiVersion: v1
kind: Pod
metadata:
  name: pod1
spec:
  containers:
    - name: contenedor1
      image: busybox
      command: [ "/bin/sh", "-c", "sleep 1000000" ]
      volumeMounts:
      - name: volumen-config-map
        mountPath: /etc/config-map
  volumes:
    - name: volumen-config-map
      configMap:
        name: config-volumen
  restartPolicy: Never
```
```
kubectl apply -f .
```
![image](https://github.com/user-attachments/assets/5972254a-2d4e-48dd-b32b-3cbfe8a9e67e)

## Ingresamos dentro de nuestro pod y consultamos el volumen.
```
kubectl exec -it pod1 sh
```
![image](https://github.com/user-attachments/assets/d0067b75-b3f1-476c-b596-3b365e45a95b)
