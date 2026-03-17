# integration-jenkins-kubernetes
# Título
Integración de Jenkins en Kubernetes

## Comenzando 🚀
_Estas instrucciones te permiten obtener una copia del proyecto en funcionamiento en tu máquina local para propósitos de desarrollo y pruebas._

### 🛠️ Tecnologías utilizadas
- Consola de PowerShell para la ejecución de comandos
- Editor Notepad o Bloc de Notas para la creación de los archivos de despliegue


### Instalación 🔧 Pruebas ⚙️ y Despliegues 📦
Primero arrancamos minikube – minikube start

<img width="688" height="262" alt="image" src="https://github.com/user-attachments/assets/1329c035-49c8-46db-b117-23d319d29e89" />

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


Paso 3: Creamos el archivo volume.yaml y copiamos el siguiente manifiesto de volumen persistente.
<img width="348" height="822" alt="image" src="https://github.com/user-attachments/assets/48419dcf-dc87-4d22-a444-f69ab4840f68" />

<img width="533" height="235" alt="image" src="https://github.com/user-attachments/assets/107bd66d-af8c-46ec-a7e3-45fb7e09d52b" />

Copiamos el archivo volume.YAML a la ruta C:\Users\6002336\.kube

Puede obtener el nombre de host del nodo trabajador mediante el archivo kubectl
kubectl get nodes

Vamos a crear el volumen usando kubectl

kubectl create -f volume.yaml

<img width="751" height="62" alt="image" src="https://github.com/user-attachments/assets/575fd786-7562-4c62-9e25-fd584d4d59b8" />

<img width="1016" height="451" alt="image" src="https://github.com/user-attachments/assets/239e7193-0972-42b6-b2b1-d2c4b0701674" />

Vemos que se ha creado el volumen y nos aparece en Minikube dashboard - configuración y almacenamiento – storage classes – local-storage.

Paso 4: Creamos un archivo de implementación llamado deployment.yaml y copiamos el siguiente manifiesto de implementación.

<img width="357" height="822" alt="image" src="https://github.com/user-attachments/assets/6e74423e-fec6-4371-a54b-36cbe65d5d2e" />

<img width="345" height="266" alt="image" src="https://github.com/user-attachments/assets/6f372788-6096-4176-bd4f-a7c92c2e8507" />

En esta implementación de Jenkins Kubernetes, se ha utilizado lo siguiente:
- SecurityContext --> para que el pod de Jenkins pueda escribir en el volumen persistente local.
- Sonda de actividad y preparación para monitorear el estado del pod de Jenkins.
- Volumen persistente local basado en la clase de almacenamiento local que contiene la ruta de datos de Jenkins /var/jenkins_home.

<img width="442" height="211" alt="image" src="https://github.com/user-attachments/assets/09c12848-6b28-4405-a2de-f0af3f162b98" />

Copiamos el archivo deployment.YAML a la ruta C:\Users\6002336\.kube

Creamos la implementación mediante kubectl

kubectl apply –f deployment.yaml

<img width="421" height="47" alt="image" src="https://github.com/user-attachments/assets/fd37f503-4b59-4d43-8d54-869f600a40c9" />

<img width="1002" height="513" alt="image" src="https://github.com/user-attachments/assets/26ae4b8e-ed50-422a-a1cd-296fcc7ba8c0" />

Vemos que se ha creado el deployment(despliegue) de jenkins en Minikube Dashboard – Cargas de trabajo - deployments

Comprobamos el estado de implementación con kubectl get deployments –n devops-tools.

<img width="506" height="48" alt="image" src="https://github.com/user-attachments/assets/b0506711-d922-4f75-ae51-3a7330af5ca9" />

Se pueden obtener los detalles de implementación con el siguiente comando: kubectl describe deployments –namespace=devops-tools

<img width="797" height="655" alt="image" src="https://github.com/user-attachments/assets/c9e413c5-e1b9-4fd4-b875-d98f955a186b" />


ACCESO A JENKINS MEDIANTE EL SERVICIO KUBERNETES:

Creamos el archivo service.yaml y copiamos el siguiente manifiesto de servicio.

<img width="313" height="391" alt="image" src="https://github.com/user-attachments/assets/7d2c8e46-179b-4f8d-a15c-7746497a33a9" />

<img width="611" height="279" alt="image" src="https://github.com/user-attachments/assets/a2f69cc6-0c49-45ce-a13c-c27f6f2b505d" />

Copiamos el archivo service.YAML a la ruta C:\Users\6002336\.kube

Creamos el servicio Jenkins usando kubectl: kubectl apply –f service.yaml

<img width="420" height="36" alt="image" src="https://github.com/user-attachments/assets/6b30aace-cbcc-47e4-ac93-e735566fbaef" />

<img width="1139" height="449" alt="image" src="https://github.com/user-attachments/assets/ebac99ea-6167-4021-ae9a-320a502c29f0" />

Vemos que aparece el servicio jenkins-service en Minikube Dashboard – Service – Servicios.

Ahora, al navegar a cualquiera de las IP de nodo en el puerto 32000, podrá acceder al panel de control de Jenkins.
http://<node-ip>:32000

Jenkins le pedirá la contraseña de administrador inicial cuando acceda al panel por primera vez.

Puede obtenerlo de los registros del pod, ya sea desde el panel de control de Kubernetes o desde la CLI. Puede obtener los detalles del pod usando el siguiente comando CLI.

<img width="489" height="48" alt="image" src="https://github.com/user-attachments/assets/a721775f-1f86-4b63-9c3c-5db109f512bd" />

kubectl get pods –namespace=devops-tools



## Licencia 📄
Bajo licencia GNU General Public License v3.0


## Autor
Alejandro Velaz

🎓 Formación: ASIR
