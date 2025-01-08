# StatefulSets
- Los StatefulSets sirven para gestionar aplicaciones con estado o Stateful
- Estas aplicaciones básicamente deben almacenar datos y ocuparse de que se guarden y se gestionen correctamente.
- Por ejemplo todas las bases de datos como mysql ,Oracle ,PostgreSQL, etc son ejemplos claros de aplicaciones con estado.

## Diferencias con los Deployments.
### Deploys.
- Los Deployment reciben nombres aleatorios
- Son totalmente intercambiables
![image](https://github.com/user-attachments/assets/964569f6-28a1-44ca-b510-4d5ffe5548c0)

- Si uno se elimina, se crea uno nuevo completamente
- Si bajamos el número de réplicas, se elimina cualquiera de los POD
![image](https://github.com/user-attachments/assets/3e622a54-cd72-4d2f-9905-b458cd9ba97b)

### StatefulSets
- En realidad un StatefulSet no es nada más que un control de kubernetes que se utiliza para ejecutar PODS que se encargan de las aplicaciones con estado.
- Una de sus principales características es que a los PODS se les asigna una identidad concreta , no aleatoria como pasa con los Deployments.
![image](https://github.com/user-attachments/assets/3d2cdefe-9115-42b0-b1af-bb640a1dea88)

- Veremos que cuando se replica un POD Stateful en realidad se clonan también los datos del POD
- Se incrementan de forma secuencial
- Los statefulSets no son intercambiables
- Si se borra uno de ellos se vuelve a recrear
- Si bajamos el número de réplicas siempre comienza por el último
![image](https://github.com/user-attachments/assets/301d3683-6d8d-4d02-a671-7030a04bc3f0)

- Si añadimos una nueva réplica siempre se copia el anterior
![image](https://github.com/user-attachments/assets/5dd20b49-f883-466a-8239-4df87b63fe15)

- Cada POD, tiene también su propio nombre DNS dentro del servicio.
![image](https://github.com/user-attachments/assets/07b4396d-143f-438a-bc98-4af687fafb0a)


## Ejemplo PODS de tipo statefulsets.
- Los PODS de tipo StatefulSet no comparten datos. Cada uno de ellos maneja su propio volumen persistente
![image](https://github.com/user-attachments/assets/6058268b-5158-4fe3-8f58-0898d7241dd1)

- Por ejemplo en el caso de una Base de Datos, tendremos un MASTER POD y el resto serán SLAVES:
![image](https://github.com/user-attachments/assets/84a8f453-59d9-49c2-9e83-aa580a12532b)

- Por tanto tiene que existir un mecanismo de sincronización entre los PODS. De ello debe encargarse el software que se ejecuta dentro.
