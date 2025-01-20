# Introduccion a RBAC.
- No existe una API especifica para gestion de usuarios en Kubernetes.
- La gestion de Usuarios se realiza de forma externa.
- Algunas opciones son:
  - Certificados.
  - Tokens.
  - Basic Authentication.
  - OAUTH2.

## Filosofia de RBAC.
![image](https://github.com/user-attachments/assets/d0ea3967-5fe1-415c-840f-c8e1d0050364)

## Foto de todo el camino de RBAC.
![image](https://github.com/user-attachments/assets/2957b638-b86e-4ff5-b8dd-91a76970e0b4)

- **Roles:** Conjunto de permisos que identifica que puede hacer en un objeto. Estan asociados a un Namespace.
- **ClusterRole:** Son como los Roles pero a nivel de Cluster. Esta por encima de los Roles.
- **RoleBinding:** Asociacion entre el Rol y el cliente.
- **ClusterRoleBinding:** Asociacion entre el ClusterRole y el cliente.
