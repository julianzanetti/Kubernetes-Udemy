# Pods.
- Es la **unidad más pequeña** y **básica** de ejecución en Kubernetes.
- Representa una instancia de tu aplicación, que puede contener uno o más contenedores.
![image](https://github.com/user-attachments/assets/c513d649-9724-48b1-822b-436872155959)

## Caracteristicas Principales:
- `Contenedor único o múltiple`: Normalmente contiene un solo contenedor, pero puede agrupar varios si necesitan compartir recursos (como red o almacenamiento).
- `Red compartida`: Todos los contenedores en un Pod comparten la misma IP, puertos y sistema de archivos si se montan volúmenes comunes.
- `Volatilidad`: Los Pods no son persistentes por sí solos. Si un Pod se elimina o falla, Kubernetes crea uno nuevo, pero con un nuevo UID y dirección IP.
- `Se gestionan mediante objetos de más alto nivel` como Deployment, StatefulSet, DaemonSet, etc.

## Ejemplo de un Pod sencillo:
```
apiVersion: v1
kind: Pod
metadata:
  name: mi-pod
spec:
  containers:
    - name: mi-contenedor
      image: nginx
      ports:
        - containerPort: 80
```
