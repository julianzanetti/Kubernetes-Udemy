# Cronjobs.
- Se ejecutan de manera planificada.
- Sintaxis de cron:
![image](https://github.com/user-attachments/assets/f1f6dc16-2061-4dc1-b624-92163fabed01)

## Ejemplo de uso:
```
apiVersion: batch/v1
kind: CronJob
metadata:
  name: cron-job1
spec:
  schedule: "* * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: job1
            image: alpine   
            command: ["sh","-c"]
            args: ["echo Me ejecuto en este momento -- $(date)"]
          restartPolicy: Never
```
> [!NOTE]
> Este cronjob esta configurado para que se ejecuto cada minuto.

![image](https://github.com/user-attachments/assets/17dc7e41-3a3f-4e93-8acf-9e26e06ac20a)
