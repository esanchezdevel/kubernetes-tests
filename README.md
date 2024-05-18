# kubernetes-tests
Project to store all things related to my Kubernetes tests

# How to install kubernetes in Linux
To install Kubernetes in Linux we have to install `microk8s` using snap, following these steps:

Install snapd:
- `sudo apt install snapd`

Install microk8s:
- `sudo snap install microk8s - - classic`

Execute this command to avoid the use of sudo each time we want to use microk8s commands
- `sudo usermod -a -G microk8s <user name>`

Add and alias of microk8s.kubectl, that way we just have to type kubectl
- `echo “alias kubectl=’microk8s.kubectl’” >> ~/.bashrc`

**Note:** Restart the PC to make all the changes take effect

# How to create deployments
Create deployment with nginx official image:
- `kubectl create deployment my-nginx --image=nginx`

Expose that nginx deployment with a ClusterIP service
- `kubectl expose deployment my-nginx --port 80`

Create deployment with apache httpd official image:
- `kubectl create deployment my-httpd --image=httpd`

# How to connect via ssh to one pod
- `kubectl exec --namespace=<namespace-name> -ti <pod-name> -- bash`

# Example of How to create a pod from a values yaml file
- `kubectl create -f values/nginx-pod.yml`

# Example of How to create a deployment with a service that expose a port
- `kubectl create -f values/nginx-deployment.yml`