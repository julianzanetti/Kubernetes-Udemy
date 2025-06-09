# Politica de Reinico en nuestro PODS.
- `restartPolicy` Se define en la especificación (spec) del Pod y aplica a todos los contenedores dentro del Pod. Existen tres valores posibles:
  - `Always`:
    - `Descripcion`: Kubernetes siempre intentará reiniciar el contenedor si se detiene, sin importar el motivo (fallo o finalización exitosa).
    - `Casos de uso`: Ideal para aplicaciones que deben estar corriendo todo el tiempo, como servidores web o APIs.
    - Default en los Deployments.
  ```
  restartPolicy: Always
  ```
  - `OnFailure`: 
    - `Descripcion`: Kubernetes solo reiniciará el contenedor si falla (es decir, si sale con un código distinto de 0).
    - `Casos de uso`: Útil para tareas que deben reintentarse al fallar, como procesos por lotes o scripts que deberían completarse con éxito.
    - Default en Jobs.
  ```
  restartPolicy: OnFailure
  ```
  - `Never`:
    - `Descripción`: Kubernetes no reinicia el contenedor sin importar si falla o termina con éxito.
    - `Casos de uso`: Bueno para tareas que deben ejecutarse una única vez, como pruebas o migraciones que no deben repetirse.
    - No recomendado para servicios de larga duración.
  ```
  restartPolicy: Never
  ```

## Ejemplo de Usos:
### Politica Always.
```
apiVersion: v1
kind: Pod
metadata:
  name: tomcat
  labels:
    app: tomcat
spec:
  containers:
   - name: tomcat     
     image: tomcat
  restartPolicy: Always
```
![image](https://github.com/user-attachments/assets/c3f924c3-1017-4124-9e64-30e9259d8777)

```
kubectl apply -f restart-always.yaml
kubectl get pods
```
![image](https://github.com/user-attachments/assets/d4747caa-76c1-4bc2-bbed-86e57308b42c)

- Si matamos el proceso del tomcat, vemos que sucede.
```
kubectl exec -it tomcat bash
catalina.sh stop
```
![image](https://github.com/user-attachments/assets/9d480555-7ce5-45bc-8073-8e51f9364516)

- Lo vuelve a reinicar:

![image](https://github.com/user-attachments/assets/877ddb44-9011-4ba0-b6f9-512849925415)

### Politica OnFailure.
- Mismo ejemplo anterior pero le cambiamos el restartPolicy a OnFailure.

![image](https://github.com/user-attachments/assets/d1859667-56fb-48a8-ba98-e094df136920)
![image](https://github.com/user-attachments/assets/1d11ec21-db26-4c0d-b908-e0519d8c93ef)

- Volvemos a parar el tomcat.
![image](https://github.com/user-attachments/assets/39537ce0-554f-4d1c-bab3-8cdd26ef1dae)

> [!NOTE]
> Como en este caso nosotros decidimos parar el tomcat, este no inicio nuevamente.

### Vamos con otro ejemplo en donde si de un error.
```
apiVersion: v1
kind: Pod
metadata:
  name: on-failure
  labels:
    app: app1
spec:
  containers:
  - name: on-failure
    image: busybox
    command: ['sh', '-c', 'echo Ejemplo de pod fallado  && exit 1']
  restartPolicy: OnFailure
```
![image](https://github.com/user-attachments/assets/97881f65-40cc-4d36-8f04-f412c7e0759f)

```
kubectl apply -f restart-onfailure.yaml
kubectl get pods
```
![image](https://github.com/user-attachments/assets/cf09b9cd-818e-4b78-9dca-4ee1bb6a5ab4)

### Como este contenedor es un loop de errores, vemos que tratar de levantarlo infinidades de veces.
![image](https://github.com/user-attachments/assets/2f168634-e8f4-4e22-b49d-d6188234f99f)

### Politica Never.
```
apiVersion: v1
kind: Pod
metadata:
  name: never
  labels:
    app: app1
spec:
  containers:
  - name: never
    image: busybox
    command: ['sh', '-c', 'echo Ejemplo de pod fallado  && exit 1']
  restartPolicy: Never
```
![image](https://github.com/user-attachments/assets/cd2a10d9-1c53-4bb1-a20a-c8f3000c982d)

```
kubectl apply -f restart-never.yaml
kubectl get pods
```
![image](https://github.com/user-attachments/assets/fd6d50f8-6e76-42b9-925c-9ae49ce5b8dd)

- Vemos que la politica never, despues del error no trato de levantar el contenedor nuevamente.
![image](https://github.com/user-attachments/assets/27ed1430-7165-4baf-b9a0-d6f3b3bee460)

