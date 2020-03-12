# Verifa-TaskB  
### Prerequisites
Installed [Kubernetes (kubectl command line)](https://kubernetes.io/docs/tasks/tools/install-kubectl/) and added PATH via environment variable. Installed [Kubernetes Helm](https://helm.sh/docs/intro/) and [Minikube](https://kubernetes.io/docs/setup/learning-environment/minikube/) via [Chocolatey](https://chocolatey.org/). [VirtualBox](https://www.virtualbox.org/) was used as the Virtual Machine provider of choice.  

### Steps Taken
1. Create Minikube Kubernetes cluster  
`minikube start — vm-driver=virtualbox`  
2. Deploy Jenkins to Minikube Kubernetes cluster  
Config files under jenkins/ was used. The Jenkins Kubernetes namespace was created with  
`kubectl apply -f jenkins/jenkins-namespace.yaml`. 
3. Create and deploy the JCasC Config Map  
`kubectl create configmap jenkins-casc-config --from-file jenkins/jenkins-casc-config.yaml --dry-run -o yaml > jenkins/jenkins-casc-config-configmap.yaml`  
`kubectl apply -f jenkins/jenkins-casc-config-configmap.yaml --namespace jenkins`  
