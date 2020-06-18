# k8s-demo
This repository is a demo for creating a app using windows docker desktop's kubernetes cluster.

There are 2 examples that setup http via nodeport and ingress
- http-NodePort (used for dev only)
- http-ingress

# Setup Local Environment
This assumes you want to use docker-desktop as your k8s cluster and ubuntu WSL as your bash

## Enable K8s from Docker desktop
Settings -> Kubernetes -> Check all options -> Apply & Restart
### NOTE:
* took a very long time to setup (walked away and came back after 30 minutes)
* Setting screen has spinning wheel (loading) so have to wait
* Noticed in a windows cmd prompt, kubectl command starts working after some time
* Can check C:\Users\<username>\ to see if .kube dir created
* Bottom of settings will show `Kubernetes starting`

## Get kubectl to run in ubuntu WSL
* After k8s installs, restart ubuntu WSL
* From WSL, your kubectl.exe will be found here:
**  /mnt/c/Program Files/Docker/Docker/resources/bin/kubectl.exe
* /etc/hosts file will be updated
* K8s cluster is setup automatically and you can tell by checking if port is open
`nc -zv kubernetes.docker.internal 6443`

## Kubectl alias and bash completion
Configure kubectl to be easier to use with proper alias and bash completion

### Local Bash Alias
Setup alias so we dont have to look for .exe. If you use to use `k` instead of kubectl, modify to your preference instead
`echo 'alias kubectl=kubectl.exe' >>~/.bashrc`

### Setup bash completion
`echo 'source <(kubectl completion bash)' >>~/.bashrc`

### Create bashcompletion file into /etc/bash_completion.d
kubectl completion bash > kubectl
sudo mv kubectl > /etc/bash_completion.d/

### Test auto complete with tabbing. See below for example commands
`kubectl get pods --all-namespaces`

# Setup k8s http-service
Creates a k8s service to be able to reachable from outside cluster
