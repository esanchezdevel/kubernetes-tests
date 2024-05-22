# kubernetes-tests
Project to store all things related to my Kubernetes tests

### How to install kubernetes in Linux
To install Kubernetes in Linux we have to install `microk8s` using snap, following these steps:
Microk8s is a kubernetes cluster that run in our local machine, and can be used to test purposes.

Install snapd:
- `sudo apt install snapd`

Install microk8s:
- `sudo snap install microk8s - - classic`

Execute this command to avoid the use of sudo each time we want to use microk8s commands
- `sudo usermod -a -G microk8s <user name>`

Add and alias of microk8s.kubectl, that way we just have to type kubectl
- `echo “alias kubectl=’microk8s.kubectl’” >> ~/.bashrc`

If we'll want to connect to external clusters, and we don't need a Kubernetes cluster, we can install the `kubectl` cli tool
- `curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"`
- `sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl`

**Note:** Take into account that if you have installed the microk8s and also install the kubectl cli, it's not needed to add the alias microk8s.kubectl to kubectl, because kubectl will works directly.
But the config used by kubectl is different than the one used by microk8s.

**Note:** Restart the PC to make all the changes take effect

### How to configure Kubeconfig to connect to remote clusters
Usually we can put the `config` file on the path `~/.kube` with the configuration that we want. That config will be used by kubectl cli tool and Helm cli tool.
But when we have microk8s installed, microk8s is taking the configuration from the file:
`/var/snap/microk8s/current/credentials/client.config`
So we'll need to add the new configuration into that file, if we want to connect external clusters using microk8s.kubectl.

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

### How to check the CPU usage of all the pods in the system
This command is useful to calculate how much CPU is consumed, when you are getting errors of insufficient CPUs for deploy pods
- `kubectl describe nodes`

