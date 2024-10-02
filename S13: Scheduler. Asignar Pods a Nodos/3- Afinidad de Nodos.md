# Afinidad de Nodos.
- La afinidad de nodos permite hacer una planificación de los post de una forma mucho más granular que con el Node Selector
- Podemos incluir reglas de distinto tipo
- Podemos indicar si la regla es para la fase de Scheduling o para la fase de  ejecución 
- También podemos indicar si es preferido u obligatorio:
  - requiredDuringSchedulingIgnoredDuringExecution
  - requiredDuringSchedulingRequiredDuringExecution
  - preferredDuringSchedulingIgnoredDuringExecution
  - preferredDuringSchedulingRequiredDuringExecution

- Se utilizan también etiquetas para identificar los nodos correctos 

## Ejemplo de uso de nodeAffinity.
```
apiVersion: v1 
kind: Pod
metadata:
  name: apache1
spec:
  affinity:
     nodeAffinity:
        requiredDuringSchedulingIgnoredDuringExecution:
          nodeSelectorTerms:
          - matchExpressions:
             - key: equipo
               operator: In
               values:
               - desarrollo-web
               - desarrollo-python
  containers:
  - name: apache1
    image: httpd
```
> [!IMPORTANT]
> Recordar agregar las labels sino no asigna el POD a ningun NODO.

```
kubectl label node ip-nodo equipo=desarrollo-web
```
