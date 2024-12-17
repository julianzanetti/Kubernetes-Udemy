# Crear un Persistent Volume y Persistent Volume Claim.
## Requisito tener un cluster con al menos 3 nodos.
![image](https://github.com/user-attachments/assets/777748c6-f13e-4877-95b0-7756880ccb53)

## Ejemplo de archivo de configuracion de PV.
```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-volume
  labels:
    type: local
    curso: kubernetes
spec:
  storageClassName: sistemaficheros
  capacity:
    storage: 10Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mnt/data"
```
![image](https://github.com/user-attachments/assets/b869dff9-ac51-42e0-ad77-123bad227c6f)

- storageClassName: Le podemos agregar el nombre que querramos, lo importante es que coincida con el PVC.
- storage: Tamaño de almacenamiento.
- HostPath: Tipo de driver a utilizar. NO UTILIZAR ESTE EN PRODUCCION.
- accessMode: Modos de acceso, ver la imagen de abajo.

![image](https://github.com/user-attachments/assets/750592ed-3ad2-41bd-b150-af55eccb9df6)

## Ejemplo de archivo de configuracion de PVC.
```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pv-claim
spec:
  storageClassName: sistemaficheros
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 3Gi
```
> [!NOTE]
> El storage del PV es el total de almacenamiento mientras el del PVC es el almacenamiento solicitado al PV y utilizado proximamente.

> [!IMPORTANT]
> storageClassName: El nombre tiene que coincider con el del PV.

![image](https://github.com/user-attachments/assets/d0db10bf-b014-4bab-ae4b-68f9ff6ad6dd)
