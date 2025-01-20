# Introduccion a las Sondas.
- Las sondas permiten realizar diagnosticos en Kubernetes.
- Existen 3 tipos de Sondas:
![image](https://github.com/user-attachments/assets/4a350425-ab54-4d1b-a2c2-000e532294b7)

- Tiene 3 tipos de comportamientos:
  - Liveness: Esta sonda nos permite saber si nuestro contenedor esta funcionando. Si no esta funcionando Kubernetes elimina el contenedor.
  - Readiness: El contenedor puede estar funcionando pero la aplicacion que esta dentro no. Dejan el contenedor inaccesible.
  - Startup: Nos indica si el contenedor arranco correctamente. Si no arranca, mata el contenedor como las liveness.
