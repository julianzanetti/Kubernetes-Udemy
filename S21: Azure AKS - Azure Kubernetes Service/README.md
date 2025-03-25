# Azure Kubernetes Services - Crear un Cluster desde 0.
## Requisitos
- Tener instalado:
  - **Azure CLI**
  - **Kubectl**

## 1- Iniciar sesion y configurar la sesion:
```
az login
az account list --output table
az account set --subscription "<ID o nombre de tu suscripción>"
```

## 2- Crear un grupo de recursos.
### Comandos:
```
az group create \
  --name aks-resource-group \
  --location eastus
```

### Consola:
- Ir a **`Resource Groups`**
- Create
- Seleccionamos la suscripcion
- Elegimos un nombre y Region.

## 3- Crear el Cluster de AKS.
### Comandos:
```
az aks create \
  --resource-group aks-resource-group \
  --name myAKSCluster \
  --node-count 2 \
  --enable-addons monitoring \
  --generate-ssh-keys

```

### Consola:
- Ir a Kubernetes Service y seleccionaos Crear Cluster.
- **`Pestaña "Básico":`**
  - Suscripción: seleccioná tu suscripción.
  - Grupo de recursos: seleccioná aks-resource-group.
  - Nombre del clúster: por ejemplo, myAKSCluster.
  - Región: misma que el resource group.
  - Disponibilidad: podés dejarlo como No availability zones.
  - Kubernetes versión: seleccioná la más reciente (estable).
  - Autenticación del clúster: dejalo con System-assigned managed identity.
![image](https://github.com/user-attachments/assets/70bd7d8e-4f01-464b-987f-e639d92546ae)
![image](https://github.com/user-attachments/assets/b0253862-5830-40a4-acd3-1635289bb803)

- **`Pestaña "Nodo":`**
  - Modo de nodo: Nodo de usuario (User node pool)
  - Tamaño de VM: por ejemplo Standard_DS2_v2 (2 vCPU, 7GB RAM)
  - Número de nodos: por ejemplo 2
![image](https://github.com/user-attachments/assets/9a84fe8e-488a-42de-bcd8-b2d350bb99d6)

- **`Pestaña "Red":`** Método de red: Azure CNI Overlay o Kubenet
![image](https://github.com/user-attachments/assets/9f627a62-dd6b-41ad-a79f-f63133a358d3)

## Conectarse al clúster.
```
az aks get-credentials \
  --resource-group aks-resource-group \
  --name myAKSCluster
```
![image](https://github.com/user-attachments/assets/a8f728e7-c7d6-4e5b-941f-882e65b1a1b4)

```
kubectl get nodes
```
![image](https://github.com/user-attachments/assets/5ff67ac3-c3fc-44a3-b29a-586d056ba884)
