# Setup k8s http-service
Creates a k8s service to be able to reachable from outside cluster

![k8s-demo-diagram](images/k8s-demo.png)

## Create namespace 'demo'
`kubectl apply -f namespace.yaml`

## Create httpd webserver Container/Pods in demo namespace
`kubectl apply -f pod.yaml`

## Create service to be Accessed Externally using NodePort
*_Dev purposes only!_*
There are 4 types of Services: ClusterIP, NodePort, LoadBalancer, Ingress. NodePort should _only be used for dev_ environments.

`kubectl apply -f svc-nodeport.yaml`

Port Spec | Description
------------ | -------------
Port | Used by other pods to access container
TargetPort | Port of the pod that the container is listening. Same as containerPort on deployment yaml
NodePort | The k8s node(s) port listening on externally for the container. Port range between 30000-32767. The set port is what will be used to access externally from k8s cluster

### Selector
`selector:` tells k8s to forward traffic to object with the metadata.label entry
* key/value pair of 'app: apache_webserver' that's how this object and the pod object links together.

## Successfully exposed http container
Go to http://localhost:31000 to see if accessible

### Commands
#### Get all pods in namespace
` kubectl get pods -n demo`

#### Get all Pods with more Details
`kubectl get pods -n demo -o wide --show-labels`

#### Get Http Pod Details in demo namespace
`kubectl describe pod http -n demo`

#### Get Services in demo namespace
`kubectl get svc -o wide -n demo`
