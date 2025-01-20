# Sonda Readiness de tipo Socket.
## Ejemplo de uso:
- ### Deploy (Vamos a desplegar un tomcat).
```
apiVersion: apps/v1 # i se Usa apps/v1beta2 para versiones anteriores a 1.9.0
kind: Deployment
metadata:
  name: tomcat-d
  labels: 
     app: tomcat
spec:
  selector:   #permite seleccionar un conjunto de objetos que cumplan las condicione
    matchLabels:
      app: tomcat
  replicas: 3 # indica al controlador que ejecute 3 pods
  template:   # Plantilla que define los containers
    metadata:
      labels:
        app: tomcat
    spec:
      containers:
      - name: tomcat
        image: apasoft/tomcat
        command: ['sh', '-c', '   sleep 40 && /opt/tomcat/bin/catalina.sh run']
        ports:
        - containerPort: 8080
        readinessProbe:
            tcpSocket:
              port: 8080
            initialDelaySeconds: 0
            periodSeconds: 5
```
> [!NOTE]
> Configuramos el contenedor para que despues de 40 segundos, arranque el tomcat.

- ### Servicio:
```
apiVersion: v1
kind: Service
metadata:
  name: tomcat-svc
  labels:
     app: tomcat
spec:
  type: NodePort
  ports:
  - port: 8080
    nodePort: 30005
    protocol: TCP
  selector:
     app: tomcat
```

## Iniciamos los pods y vemos su comportamiento
```
kubectl apply -f .
```
![image](https://github.com/user-attachments/assets/36fb9e66-f5a0-4645-8de5-2c3e8eb626a9)
![image](https://github.com/user-attachments/assets/793120d8-f33d-4288-81d8-d30217f22d19)

> [!NOTE]
> Vemos que los PODS arrancan en estado de falla, porque no tiene acceso al puerto 8080.
> Cuando levantemos el tomcat la sonda tendria que mandar la señal y los PODS arrancar.

- ### Despues de los 40 segundos:
![image](https://github.com/user-attachments/assets/221171af-75a1-4660-9cbd-e6f95f367bcc)

```
kubectl describe pod ID
```
![image](https://github.com/user-attachments/assets/8298eb3a-b839-4056-a3fc-96abf9e3ae86)

