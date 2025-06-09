# Etiquietar nuestros objetos.
## Labels.
- Son pares `clave-valor` que se asignan a objetos de Kubernetes (Pods, Services, Deployments, etc.) para identificarlos y organizarlos.
- Sirven para:
  - Agrupar recursos relacionados.
  - Seleccionar recursos desde otros objetos (como los Services o Deployments).
  - Filtrar resultados con `kubectl`.
  - Propósitos de automatización y administración.
- Ejemplo:
```
metadata:
  labels:
    app: web-app
    tier: frontend
    curso: kubernetes
```

## Selectors
- Los Selectors permiten buscar o seleccionar recursos que tienen ciertos Labels. Es como decir: “dame todos los Pods con el label app=web-app”.
- Donde se usan:
  - En los `Services` para identificar qué Pods deben exponer.
  - En los `ReplicaSets o Deployments` para manejar un conjunto de Pods.
  - En comandos `kubectl`.
- Ejemplo:
### Pod.
```
apiVersion: v1
kind: Pod
metadata:
  name: mi-pod
  labels:
    app: web
    tier: frontend
```
### Service.
```
apiVersion: v1
kind: Service
metadata:
  name: web-service
spec:
  selector:
    app: web
    tier: frontend
  ports:
    - port: 80
      targetPort: 8000
```

- Busqueda:
```
kubectl get pods -l app=web-app
```

## Annotations.
- También son pares `clave-valor`, pero a diferencia de los Labels, no se usan para seleccionar o filtrar objetos.
- Sirven para guardar metadatos adicionales que pueden ser útiles para herramientas, scripts, o humanos. Por ejemplo:
  - Información del autor.
  - Checksums
  - Tiempos de despliegue.
  - Configuraciones externas.
- Ejemplo:
```
metadata:
  annotations:
    author: "julian.zanetti"
    revision: "1.0"
    documentation: "https://midoc.com/k8s/podinfo"
```
