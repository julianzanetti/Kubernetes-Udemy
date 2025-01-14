# Jobs.
- Es un workload que se lanza en un momento determinado, terminado su trabajo finaliza el pod.
- Se usa para tareas concretas (bkps, etc.)
- No podemos modificar el fichero yaml y volver a lanzar un JOB.
## Ejemplo de uso
```
apiVersion: batch/v1
kind: Job
metadata:
  name: job1
spec:
  template:
    spec:
      containers:
      - name: job1
        image: alpine   
        command: ["sh","-c"]
        args: ["echo Estas en la maquina con el nombre $(uname -n)"]
      restartPolicy: Never
```
![image](https://github.com/user-attachments/assets/ec564228-8b68-40b7-8626-237862bce7c4)

## Probar modificar el archivo yaml y volver a lanzar.
![image](https://github.com/user-attachments/assets/46f529ad-83f7-4cf9-8025-89518cba6f0e)
> [!NOTE]
> Es necesario borrar el JOB, realizar la modificacion y volver a lanzar.

## Jobs con varias replicas.
- Las tareas la realiza de forma secuencial, es decir, espera que finalice el anterior para que arranque el siguiente.
### Ejemplo.
```
apiVersion: batch/v1
kind: Job
metadata:
  name: job2
spec:
  completions: 3
  template:
    spec:
      containers:
      - name: job1
        image: alpine   
        command: ["sh","-c"]
        args: ["echo Estas en la maquina con el nombre $(uname -n)"]
      restartPolicy: Never
```
![image](https://github.com/user-attachments/assets/e54c61cb-6c60-4736-a3a5-5e7fd22d8b4b)

## Jobs con varias replicas trabajando en paralelo.
```
apiVersion: batch/v1
kind: Job
metadata:
  name: job3
spec:
  completions: 3
  parallelism: 2
  template:
    spec:
      containers:
      - name: job1
        image: alpine   
        command: ["sh","-c"]
        args: ["echo Estas en la maquina con el nombre $(uname -n)"]
      restartPolicy: Never
```
![image](https://github.com/user-attachments/assets/9e798391-4344-4bbf-9da5-2458516f5146)
> [!NOTE]
> En el ejemplo levantamos dos PODS (parallelism: 2) de forma paralela, luego de finalizar levanto el tercero

## Job con error.
- Cuando un Job queda en estado de error, este levanta PODS hasta que sea completado o hasta el limite que nosotros brindemos.

### Ejemplo sin limite.
```
apiVersion: batch/v1
kind: Job
metadata:
  name: job4
spec:
  template:
    spec:
      containers:
      - name: job1
        image: alpine   
        command: ["sh","-c"]
        args: ["cat/etc/puff.txt"]
      restartPolicy: Never
```
![image](https://github.com/user-attachments/assets/6d29a6aa-eee4-481b-976a-3dbd555e5f53)

### Ejemplo con limite.
```
apiVersion: batch/v1
kind: Job
metadata:
  name: job4
spec:
  backoffLimit: 2
  template:
    spec:
      containers:
      - name: job1
        image: alpine   
        command: ["sh","-c"]
        args: ["cat/etc/puff.txt"]
      restartPolicy: Never
```
![image](https://github.com/user-attachments/assets/211347a9-f967-42ba-86ce-528b8bbf7d1b)

> [!NOTE]
> El backoffLimit ejecuta la cantidad que ingresemos +1.
