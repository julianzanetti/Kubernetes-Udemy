# Instalar Kubectl en linux.
## Descargamos la ultima version del binario.
```
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```
![image](https://github.com/user-attachments/assets/483883fa-b84a-4fa6-8ed6-1fcf178407d7)

## Instalamos el binario descargado (realizarlo como root).
```
install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```
![image](https://github.com/user-attachments/assets/89a5c9fd-0956-4ad8-9f17-095595ec3da2)

## Verificamos que se haya instalado correctamente.
```
kubectl version --client --output=yaml
```
![image](https://github.com/user-attachments/assets/b20d2415-7c66-420f-a847-34aad147540e)
