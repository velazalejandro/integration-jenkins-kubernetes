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
