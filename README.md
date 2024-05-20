# kubernetes-tests
Project to store all things related to my Kubernetes tests

### How to install kubernetes in Linux
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

### How to configure Kubeconfig to connect to remote clusters
Usually we can put the `config` file on the path `~/.kube` with the configuration that we want.
But when we have microk8s installed, microk8s is taking the configuration from the file:
`/var/snap/microk8s/current/credentials/client.config`
So we'll need to add the new configuration into that file.

To validate that new configuration is added, we can execute the following command:
- `kubectl config get-contexts -o=name`

Also we can execute the following command to check which context we are using now:
- `kubectl config current-context`

To switch between clusters, we can use the context name references. For example, if we have one context with name `cluster-02` that points to one remote cluster, we can execute the following command:
- `kubectl config use-context cluster-02`

And after execute that command, all the kubectl commands will be executed over that cluster

### How to create deployments
Create deployment with nginx official image:
- `kubectl create deployment my-nginx --image=nginx`

Expose that nginx deployment with a ClusterIP service
- `kubectl expose deployment my-nginx --port 80`

Create deployment with apache httpd official image:
- `kubectl create deployment my-httpd --image=httpd`

### How to connect via ssh to one pod
- `kubectl exec --namespace=<namespace-name> -ti <pod-name> -- bash`

### Example of How to create a pod from a values yaml file
- `kubectl create -f values/nginx-pod.yml`

### Example of How to create a deployment with a service that expose a port
- `kubectl create -f values/nginx-deployment.yml`

### How to get the yaml file that corresponds to one deployment without creating the deployment
The `--dry-run` flag indicates that we don't want to create the deployment, and we just want to get the yaml file needed to create that deployment
- `kubectl create deployment web --image nginx -o yaml --dry-run`
