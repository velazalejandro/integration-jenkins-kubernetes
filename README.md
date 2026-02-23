# integration-jenkins-kubernetes
# Título
Integración de Jenkins en Kubernetes

## Comenzando 🚀
_Estas instrucciones te permiten obtener una copia del proyecto en funcionamiento en tu máquina local para propósitos de desarrollo y pruebas._

### Pre-requisitos 📋
_Que cosas necesitas para instalar el software y como instalarlas_
- Manejar la consola de PowerShell para la ejecución de comandos.
- Manejar el editor Notepad o Bloc de Notas para la creación de los archivos de despliegue.


### Instalación 🔧 Pruebas ⚙️ y Despliegues 📦
INTEGRACIÓN DE JENKINS EN KUBERNETES:

<img width="688" height="262" alt="image" src="https://github.com/user-attachments/assets/1329c035-49c8-46db-b117-23d319d29e89" />

Primero arrancamos minikube – minikube start

<img width="443" height="32" alt="image" src="https://github.com/user-attachments/assets/e9ec45ea-1de4-4115-891a-15604968e0fe" />

Paso 1: Creamos un espacio de nombres para Jenkins. Es bueno categorizar las herramientas de DevOps como un espacio de nombres separado de otras aplicaciones.
kubectl create namespace devops-tools

<img width="937" height="662" alt="image" src="https://github.com/user-attachments/assets/573c72dc-9369-4595-ab1c-333579970b3f" />

También vemos que en la página minikube dashboard en Cluster – Espacios de nombre – vemos que aparece devops-tools.

Paso 2: Creamos un archivo serviceAccount.yaml y copiamos el siguiente manifiesto de cuenta de servicio de administración.

<img width="350" height="548" alt="image" src="https://github.com/user-attachments/assets/39ac4d92-e372-43e8-94be-50825e8974cc" />

<img width="648" height="273" alt="image" src="https://github.com/user-attachments/assets/cc5741e7-b772-455e-8e64-417e2ae93782" />

<img width="993" height="371" alt="image" src="https://github.com/user-attachments/assets/59c28c52-7fdd-4c1c-89a3-1d244db18ca7" />

cluster roles – jenkins-admin

<img width="438" height="149" alt="image" src="https://github.com/user-attachments/assets/334086d2-1cd6-4d5e-ad9b-e032d46d9666" />

Copiamos el fichero serviceAccount.YAML a la ruta C:\Users\6002336\.kube

El 'serviceAccount.yaml' crea un clusterRole 'jenkins-admin', ServiceAccount 'jenkins-admin' y vincula el 'clusterRole' a la cuenta de servicio.
El rol de clúster 'jenkins-admin' tiene todos los permisos para administrar los componentes del clúster. También puede restringir el acceso especificando acciones de recursos individuales.
Ahora crea la cuenta de servicio usando kubectl.

<img width="846" height="103" alt="image" src="https://github.com/user-attachments/assets/7e1468b4-6338-4af4-9ca5-18f29d341cad" />

cd C:\Users\6002336\.kube

kubectl apply –f serviceAccount.yaml

<img width="994" height="594" alt="image" src="https://github.com/user-attachments/assets/cf8ba81b-f596-42be-bdc6-04285780b0d6" />

Visualizamos en Kubernetes Dashboard – Cluster – Cuentas de servicio – vemos que se ha añadido correctamente la cuenta de servicio jenkins-admin.

<img width="995" height="597" alt="image" src="https://github.com/user-attachments/assets/a53f4b94-9433-4d8f-a169-7018883f419e" />
<img width="571" height="227" alt="image" src="https://github.com/user-attachments/assets/99afbd1e-d7ab-496b-8dba-dc0152993f0b" />


