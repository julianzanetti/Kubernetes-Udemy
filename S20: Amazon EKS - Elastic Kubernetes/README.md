# Cluster de EKS.
## Crear el stack de Red (VPC y Subredes).
- Este es el primer paso para comenzar con nuestra creacion de un CLUSTER de EKS.
- Tenemos que crear nuestra **`VPC`** con sus respectivas **`subredes`**, las puertas de enlace (**`Internet Gateway`**) y su tabla de enrutamiento.

## Crear los Roles IAM para EKS.
- El primer rol a seleccionar esta vinculado al Servicio del Cluster y es el **`AmazonEKSClusterPolicy`**.
- Luego seleccionaremos el rol vinculado al Servicio de Nodos y son: **`AmazonEC2ContainerRegistryReadOnly`**, **`AmazonEKS_CNI_Policy`** y **`AmazonEKSWorkerNodePolicy`**

## Crear el cluster de EKS.
- Una ves creado toda la infraestructura y dado los accesos/permisos necesarios, ya podemos crear nuestro CLUSTER.

## Configurar Nodos de Trabajo
- Creamos nuestro grupo de Nodos administrados

## Configurar el acceso al Cluster.
- En nuestra maquina en la cual vamos a estar trabajando, configuramos nuestro **`kubectl`** para EKS.
```
aws eks update-kubeconfig --name mi-cluster
```

- Verificamos que se haya configurado correctamente:
```
kubectl get nodes
```
