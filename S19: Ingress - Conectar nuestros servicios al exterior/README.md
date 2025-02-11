# Ingress.
- ES UN COMPONENTE QUE GESIONA EL ACCESO DESDE EL EXTERIOR AL CLUSTER DE KUBERNETES
- TAMBIÉN BALANCEA EL TRAFICO ENTRE LOES ENDPOINTS
- IMPLEMENTA ENCRIPTACION A TRAVÉS DE HHTPS.

![image](https://github.com/user-attachments/assets/04666deb-96fa-4d66-a613-57c7656c5d6a)

## Ejemplo de manifiesto de Ingress.
![image](https://github.com/user-attachments/assets/fb736924-03d3-4882-afa6-f85963dfa340)
![image](https://github.com/user-attachments/assets/dbaa659a-319a-41f0-b7d6-6525f5e520c4)
![image](https://github.com/user-attachments/assets/42898bca-3d9e-4e02-8ca6-28c519bdd0d0)

## DefaultBackend
- Si un ingress no tiene reglas o no cuadra ninguna, las peticiones se mandan a un Backend por defecto
- Normalmente se usa el propio Ingress Controller para definirlo.

![image](https://github.com/user-attachments/assets/806134c6-fffd-4c9f-8447-befe6910405a)

## Tipos de PATH
- ### Hay 3 tipos soportados:
  - ImplementationSpecific: Se implementa por parte del propio controller y nos permiten configuraciones más complejas
  - Exact: en este caso el path debe de coincidir exactamente incluido mayúsculas y minúsculas.
  - Prefix: el path está basado en un prefijo dividido por la barra ”/”. distingue entre mayúsculas y minúsculas y se determina elemento a elemento.

- ### Ejemplos:
![image](https://github.com/user-attachments/assets/19e3e0bc-8467-4fde-a268-331ce046ca30)
![image](https://github.com/user-attachments/assets/b2e1772a-c88c-468d-9eaf-b994fa8d4fd4)

- ### Un solo HOST con varios servicios.
![image](https://github.com/user-attachments/assets/e252bde9-a7b6-4f16-b84b-7e874a948b27)
