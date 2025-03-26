# Elastic Kubernetes - Cluster en EKS desde 0.
## Crear el stack de Red (VPC y Subredes).
- Este es el primer paso para comenzar con nuestra creacion de un CLUSTER de EKS.
- Tenemos que crear nuestra **`VPC`** con sus respectivas **`subredes`**, las puertas de enlace (**`Internet Gateway`**) y su tabla de enrutamiento.

### Por Terminal:
- VPC:
```
aws ec2 create-vpc --cidr-block 10.0.0.0/16
```
- SubRedes:
```
aws ec2 create-subnet --vpc-id <VPC_ID> --cidr-block 10.0.1.0/24 --availability-zone sa-east-1a
aws ec2 create-subnet --vpc-id <VPC_ID> --cidr-block 10.0.2.0/24 --availability-zone sa-east-1b
```
- Gateway:
```
aws ec2 create-internet-gateway
aws ec2 attach-internet-gateway --vpc-id <VPC_ID> --internet-gateway-id <InternetGatewayId>
```
- Configurar la tabla de rutas:
```
aws ec2 describe-route-tables --filters "Name=vpc-id,Values=<VPC_ID>"
aws ec2 create-route --route-table-id <RouteTableId> --destination-cidr-block 0.0.0.0/0 --gateway-id <InternetGatewayId>
```

## Crear los Roles IAM para EKS.
> [!NOTE]
> Primero se crea el ROL y luego se asocia los permisos necesarios.

El primer rol a seleccionar esta vinculado al Servicio del Cluster y es el **`AmazonEKSClusterPolicy`**.
- **`ROL:`**
```
aws iam create-role --role-name EKSClusterRole --assume-role-policy-document file://eks-cluster-trust-policy.json
```
- **`PERMISOS:`**
```
aws iam attach-role-policy --role-name EKSClusterRole --policy-arn arn:aws:iam::aws:policy/AmazonEKSClusterPolicy
```

Luego seleccionaremos el rol vinculado al Servicio de Nodos y son: **`AmazonEC2ContainerRegistryReadOnly`**, **`AmazonEKS_CNI_Policy`** y **`AmazonEKSWorkerNodePolicy`**
- **`ROL:`**
```
aws iam create-role --role-name EKSNodeRole --assume-role-policy-document file://eks-node-trust-policy.json
```
- **`PERMISOS:`**
```
aws iam attach-role-policy --role-name EKSNodeRole --policy-arn arn:aws:iam::aws:policy/AmazonEKSWorkerNodePolicy
aws iam attach-role-policy --role-name EKSNodeRole --policy-arn arn:aws:iam::aws:policy/AmazonEC2ContainerRegistryReadOnly
aws iam attach-role-policy --role-name EKSNodeRole --policy-arn arn:aws:iam::aws:policy/AmazonEKS_CNI_Policy
```

## Crear el cluster de EKS.
- Una ves creado toda la infraestructura y dado los accesos/permisos necesarios, ya podemos crear nuestro CLUSTER.
```
aws eks create-cluster --name mi-cluster --role-arn arn:aws:iam::<ACCOUNT_ID>:role/EKSClusterRole --resources-vpc-config subnetIds=<SUBNET1>,<SUBNET2>,securityGroupIds=<SECURITY_GROUP_ID>
```
- Verificar su estatus:
```
aws eks describe-cluster --name mi-cluster --query "cluster.status"
```

## Configurar Nodos de Trabajo
- Creamos nuestro grupo de Nodos administrados
```
aws eks create-nodegroup --cluster-name mi-cluster --nodegroup-name mi-nodo --subnets <SUBNET1> <SUBNET2> --node-role arn:aws:iam::<ACCOUNT_ID>:role/EKSNodeRole --scaling-config minSize=1,maxSize=3,desiredSize=2 --ami-type AL2_x86_64 --instance-types t3.medium
```

## Configurar el acceso al Cluster.
- En nuestra maquina en la cual vamos a estar trabajando, configuramos nuestro **`kubectl`** para EKS.
```
aws eks update-kubeconfig --name mi-cluster
```

- Verificamos que se haya configurado correctamente:
```
kubectl get nodes
```
