# Verifa-TaskB  
Personal VSCode project fork including the Jenkinsfile can be found [here](https://github.com/geonhuiy/vscode).  

### Prerequisites
Installed [Kubernetes (kubectl command line)](https://kubernetes.io/docs/tasks/tools/install-kubectl/). Installed [Kubernetes Helm](https://helm.sh/docs/intro/) and [Minikube](https://kubernetes.io/docs/setup/learning-environment/minikube/) via [Chocolatey](https://chocolatey.org/). [VirtualBox](https://www.virtualbox.org/) was used as the Virtual Machine provider of choice.  

### Steps Taken
1. Create Minikube Kubernetes cluster  
`minikube start — vm-driver=virtualbox`  

2. Deploy Jenkins to Minikube Kubernetes cluster  
Config files under jenkins/ was used. The Jenkins Kubernetes namespace was created with  
`kubectl apply -f jenkins/jenkins-namespace.yaml`.  

3. Create and deploy the JCasC Config Map  
`kubectl create configmap jenkins-casc-config --from-file jenkins/jenkins-casc-config.yaml --dry-run -o yaml > jenkins/jenkins-casc-config-configmap.yaml`  
`kubectl apply -f jenkins/jenkins-casc-config-configmap.yaml --namespace jenkins`.  

4. Install the Jenkins Helm Chart  
Since `helm init` and Tiller was removed at Helm v3.0,  
Added `stable` repo with `helm repo add stable https://kubernetes-charts.storage.googleapis.com`.  
Jenkins Helm Chart was installed with `helm install jenkins -f jenkins/jenkins-values.yaml stable/jenkins --namespace jenkins`.  
The Jenkins instance could be opened at http://192.168.99.104:32000/login.  

The pipeline project pointed at the forked repository was initialized to read and execute from the Jenkinsfile from the root of the project directory. However, the pipeline seems to fail at building and times out upon reaching `git fetch`.  
