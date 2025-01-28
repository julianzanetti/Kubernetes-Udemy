# Configurar certificados para el acceso de un Usuario.
## Creamos un directorio para almacenar todos los ficheros.
```
mkdir certs
cd certs
```

##  Generamos una clave privada para un usuario llamado “desa1”. Se crea un fichero denominado desa1.key
```
openssl genrsa -out desa1.key 4096
```

##  Vamos a crear un archivo de configuración para gestionar la petición de solicitud de firma. Le llamamos “desa1.csr.cnf”.
```
[ req ]
default_bits = 2048
prompt = no
default_md = sha256
distinguished_name = dn
[ dn ]
CN = desa1
O = desarrollo
[ v3_ext ]
authorityKeyIdentifier=keyid,issuer:always
basicConstraints=CA:FALSE
keyUsage=keyEncipherment,dataEncipherment
extendedKeyUsage=serverAuth,clientAuth
```

##  Ahora hacemos la solicitud de firma. Con este commando se genera un fichero “desa1.csr".
```
openssl req -config desa1.csr.cnf -new -key desa1.key -nodes -out desa1.csr
```
![image](https://github.com/user-attachments/assets/bd84e88e-b7ba-4b81-a690-feebfd97fcb3)

## Generamos una llamada al cluster de Kubernetes para aprobar o rechazar la petición de firma.
- En este caso se crea un objeto de tipo CertificateSigningRequest y le pasamos desa1.csr codificado en base 64.
```
cat <<EOF | kubectl apply -f -
apiVersion: certificates.k8s.io/v1
kind: CertificateSigningRequest 
metadata:
 name: desa1-firma # nombre de la peticion
spec:
 groups:
 - system:authenticated
 request: $(cat desa1.csr | base64 | tr -d '\n')
 signerName: kubernetes.io/kube-apiserver-client
 usages:
 - digital signature
 - key encipherment
 - server auth
 - client auth
EOF
```
![image](https://github.com/user-attachments/assets/c7196ead-47bd-452a-975e-9f4fb6d4669a)

## Comprobamos que el certificado está:
```
kubectl get csr
```
![image](https://github.com/user-attachments/assets/4f33f4d6-ef1a-4aa9-980a-5f4f1a42573a)

## Aprobamos el certificado.
```
kubectl certificate approve desa1-firma
```
![image](https://github.com/user-attachments/assets/a7fe078c-1c69-4cd0-9edc-fa6ff1ec8e5d)

## Lo descargamos en el fichero desa1.crt en el directorio certs.
```
kubectl get csr desa1-firma -o jsonpath='{.status.certificate}' | base64 --decode > desa1.crt
```
![image](https://github.com/user-attachments/assets/82937dbf-9457-4d34-9c8a-15b7ab952a1d)

## Probamos sin crear otro usuario de linux (modo de ejemplo).
- ### Creamos un directorio llamado “.kube” dentro del directorio “certs” y copiamos el archivo config.
![image](https://github.com/user-attachments/assets/89d3c453-f0c4-4338-bc9a-cb0fa33dd063)

- ### Lo dejamos de forma que pueda acceder al cluster con el usuario “desa1”
```
apiVersion: v1
clusters:
- cluster:
 certificate-authority: /home/kubernetes/.minikube/ca.crt
 server: https://192.168.99.101:8443
 name: minikube
contexts:
- context:
 cluster: minikube
 namespace: ventas
 user: desa1
 name: desa1-context
current-context: desa1-context
kind: Config
preferences: {}
users:
- name: desa1
 user:
 client-certificate: /home/kubernetes/certs/desa1.crt
 client-key: /home/kubernetes/certs/desa1.key
```

- ### Probamos cambiando el kube-config al nuevo.
```
kubectl --kubeconfig=/home/Kubernetes/RBAC/certs/.kube/config get pods
```
![image](https://github.com/user-attachments/assets/65df58d7-f7f1-4ba3-8e1a-55897aa4e7cd)

- Al no tener permisos nos da un error.
