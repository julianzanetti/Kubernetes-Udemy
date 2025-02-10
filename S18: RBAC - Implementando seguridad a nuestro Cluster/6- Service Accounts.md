# Service Accounts.
- Este recurso en realidad provee de una identidad a los procesos que se están ejecutando dentro de un POD.
- Cuando accedemos a la API Server desde fuera lo hacemos normalmente con un usuario con algún tipo de autenticación.
- Cuando un POD necesita acceder al API Server se implementa a través de una `service account`.
- Son gestionados por la API de kubernetes y se asocian habitualmente a NameSpaces específicas.

## 
