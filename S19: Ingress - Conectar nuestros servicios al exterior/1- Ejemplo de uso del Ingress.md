# Ejemplo de uso del Ingress.
## Ingress con un servicio.
- ### Creamos un pod con la imagen de apache.
```
kubectl run apache --image=httpd
```

- ### Creamos un servicio para el POD.
```
kubectl expose pod apache --type=NodePort --port=80
```

- ### Creamos el ingress.
```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
   name: ingress-apache
   annotations:
     nginx.ingress.kubernetes.io/rewrite-target: /
spec:
   rules:
   - host: curso.prueba.com
     http:
       paths:
       - path: /apache
         pathType: Exact
         backend:
           service:
             name: apache
             port:
               number: 80
```
> [!NOTE]
> El host es el DNS que nosotros tendremos que brindar, este DNS como sabemos tiene que estar vinculado a la IP de nuestro cluster.

- ### Probamos Ingresar.
![image](https://github.com/user-attachments/assets/9236b326-5959-40f1-b1ea-f5558fcac26a)

## Ingress con dos servicios.
- ### Creamos un POD con la imagen de nginx.
```
kubectl run nginx --image=httpd
```

- ### Creamos un servicio para el POD.
```
kubectl expose pod nginx --type=NodePort --port=80
```

- ### Creamos el ingress.
```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
   name: ingress-apache-nginx
   annotations:
     nginx.ingress.kubernetes.io/rewrite-target: /
spec:
   rules:
   - host: curso.prueba.com
     http:
       paths:
       - path: /apache
         pathType: Exact
         backend:
           service:
             name: apache
             port:
               number: 80
       - path: /nginx
         pathType: Exact
         backend:
           service:
             name: nginx
             port:
               number: 80
```

- ### Probamos Ingresar.
![image](https://github.com/user-attachments/assets/f714f38f-8ba8-46a2-8ba1-e42f009e6899)

## Ingress con varios servicios.
- ### Creamos dos POD en este caso con imagenes de DockerHub.
```
kubectl run blog --image=apasoft/blog
kubectl run web --image=apasoft/web
```

- ### Creamos un servicio para los POD.
```
kubectl expose pod blog --type=NodePort --port=8080
kubectl expose pod web --type=NodePort --port=80
```

- ### Creamos el ingress.
```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
   name: ingress-multi-hosts
   annotations:
     nginx.ingress.kubernetes.io/rewrite-target: /
spec:
   rules:
   - host: desarrollo.curso.com
     http:
       paths:
       - path: /apache
         pathType: Exact
         backend:
           service:
             name: apache
             port:
               number: 80
       - path: /nginx
         pathType: Exact
         backend:
           service:
             name: nginx
             port:
               number: 80
   - host: produccion.curso.com
     http:
       paths:
       - path: /blog
         pathType: Prefix
         backend:
           service:
             name: blog
             port:
               number: 8080
       - path: /web
         pathType: Prefix
         backend:
           service:
             name: web
             port:
               number: 80
```

- ### Probamos Ingresar.
**`desarrollo.curso.com/apache`**

![image](https://github.com/user-attachments/assets/97affeb9-7c38-4322-bb3c-7bf0bdbdabcc)

**`desarrollo.curso.com/nginx`**

![image](https://github.com/user-attachments/assets/fdad61e0-300c-4dff-85ae-da8d5e154555)

**`produccion.curso.com/blog`**

![image](https://github.com/user-attachments/assets/924141b3-b800-45a0-979f-cb4d6096586a)

**`produccion.curso.com/web`**

![image](https://github.com/user-attachments/assets/c0690fc2-cfac-4c68-9c6d-63ee6f94111b)
