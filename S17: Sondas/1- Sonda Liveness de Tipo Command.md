# Sonda Liveness de Tipo Command.
## Archivo de ejemplo:
```
apiVersion: v1
kind: Pod
metadata:
  labels:
    test: liveness
  name: sonda-liveness
spec:
  containers:
  - name: pod-liveness
    image: ubuntu
    args:
    - /bin/sh
    - -c
    - mkdir /tmp/prueba; sleep 30; rm -rf /tmp/prueba; sleep 600
    livenessProbe:              ## Clausula para saber que trabajamos con una sonde de tipo liveness.
      exec:
        command:
        - ls
        - /tmp/prueba
      initialDelaySeconds: 5    ## Cuanto tiempo tarda la sonda en ponerse en marcha.
      periodSeconds: 5          ## Cada cuanto tiempo la sonda este preguntando.
```
> [!NOTE]
> Esta prueba indica que creamos un directorio en el /tmp/pruebas, durante 30 segundos la sonda verifica que el directorio existe.
> Luego de los 30 segundos se borra el directorio y la sonda dara aviso del mismo. Luego procedera a borrar el contenedor.

![image](https://github.com/user-attachments/assets/c6e72671-0a4a-46cc-b7f9-f657fcf148fa)
![image](https://github.com/user-attachments/assets/b2d7adbc-3199-4d15-b63e-e2c54319aa7c)

### Mensaje de error:
![image](https://github.com/user-attachments/assets/eb13a823-84b2-4c14-b180-06264ccea3dc)

### Vuelve a levantar el contenedor:
![image](https://github.com/user-attachments/assets/4e851cc3-52be-4932-96dd-3f0a5326a74a)

### Vuelve a matar el contenedor y levantarlo nuevamente:
![image](https://github.com/user-attachments/assets/11d09580-bd7e-4796-aae5-0aff5f27cf95)
