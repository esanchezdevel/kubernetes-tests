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

