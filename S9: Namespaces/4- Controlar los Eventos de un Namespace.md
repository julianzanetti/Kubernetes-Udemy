# Controlar los Eventos de un Namespace.
## Creamos un nuevo Namespace.
```
kubectl create namespace desarrollo
```
![image](https://github.com/user-attachments/assets/3a68ac8a-40d2-407e-af3b-83a286463592)

## Vemos los eventos de este namespace.
```
kubectl get events --namespace desarrollo
```
![image](https://github.com/user-attachments/assets/a76e2c79-88f6-4631-9842-e7a95a0edbe3)

## Creamos un pod de ejemplo para este namespace y vemos los eventos nuevamente.
```
kubectl run apache --image=httpd
kubectl get pods -n desarrollo
kubectl get events --namespace desarrollo
```
![image](https://github.com/user-attachments/assets/714b1538-f86b-4108-9959-58a99de0d41e)

## Creamos otro pod pero con una imagen inexistente.
```
kubectl run apache2 --image=httpd2
kubectl get pods -n desarrollo
kubectl get events --namespace desarrollo
```
![image](https://github.com/user-attachments/assets/54c42f41-fb26-4cfb-bb30-58dc3b5d786b)

## Filtramos nuestro evento por el tipo "Warning".
```
kubectl get events --namespace desarrollo --field-selector type='Warning'
```
![image](https://github.com/user-attachments/assets/ca78016c-c885-4f7a-b474-1a51d6ac27e3)

## Ver los eventos en directo.
```
kubectl get events --namespace desarrollo -w
```
![image](https://github.com/user-attachments/assets/f65b5d39-cfe5-430b-b119-21040733da41)

## Filtrar por los que fallaron.
```
kubectl get events --namespace desarrollo -w --field-selector reason='Failed'
```
![image](https://github.com/user-attachments/assets/f545920c-3612-45dc-b9de-e05ccbec5a40)
