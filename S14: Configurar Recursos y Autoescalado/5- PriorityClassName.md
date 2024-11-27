# PriorityClassName - Dar prioridad a nuestros Pods.
## Ver cuales son nuestros PriorityClass.
```
kubectl get pc
```
![image](https://github.com/user-attachments/assets/d7a5b006-1910-4e4b-8701-a801eb310b47)

## Ejemplo de una configuracion de priorityclass.
```
apiVersion: scheduling.k8s.io/v1
kind: PriorityClass
metadata:
  name: produccion
value: 100
preemptionPolicy: PreemptLowerPriority
globalDefault: false
description: "Pods para entornos de Producción."

---

apiVersion: scheduling.k8s.io/v1
kind: PriorityClass
metadata:
  name: desarrollo
value: 50
preemptionPolicy: PreemptLowerPriority
globalDefault: false
description: "Pods para entornos de desarrollo."
```
![image](https://github.com/user-attachments/assets/b26c469c-ddb1-4796-8046-f409ccdcf810)
