# Crear, ver las propiedades, ejecutar comandos, ver los logs y visualizar desde internet el POD.
## Crear nuestro primer POD.
```
kubectl run nombre_pod --image=imagen
```
![image](https://github.com/user-attachments/assets/46c2614e-8d89-4507-8046-71e976360274)

## Ver nuestros PODS creados.
```
kubectl get pods
```
![image](https://github.com/user-attachments/assets/8f3cd818-8bbc-4beb-8035-65b3d7b24f96)

## Describir el POD creado recientemente.
```
kubectl describe pod nombre_pod
```
![image](https://github.com/user-attachments/assets/1bb92470-9ac4-4c1e-ab75-ed75485f159c)

## Lanzar un comando contra el POD.
```
kubectl exec nombre_pod -- comando
```
![image](https://github.com/user-attachments/assets/f7f78092-37f0-4234-9e55-559bb59aec9a)

## Entrar en modo interativo al POD.
```
kubectl exec nombre_pod -it -- bash
```
![image](https://github.com/user-attachments/assets/22bde345-255c-4065-820e-061b930a8f46)

## Ver los logs de un POD.
```
kubectl logs nombre_pod
```
![image](https://github.com/user-attachments/assets/d3d40209-d3d5-439c-9474-0c55f0cb8db2)

## Visualizar si el POD esta arriba desde internet.
```
kubectl proxy nombre_pod
```
![image](https://github.com/user-attachments/assets/2d351f9e-7381-47fd-9d1e-09dbd84b8546)
![image](https://github.com/user-attachments/assets/a34463a3-5859-44b4-a107-73b881671826)
