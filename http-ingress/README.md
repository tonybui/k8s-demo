# Setup k8s http using ingress to /demo endpoint
Creates a k8s service to be able to reachable from outside cluster

/demo -> nginx-ingress -> http svc -> app: http at port 80 

## Create namespace 'demo'
`kubectl apply -f namespace.yaml`

## Create httpd webserver Container/Pods in demo namespace
`kubectl apply -f pod.yaml`

## Create service to be Accessed Externally using Ingress
`kubectl apply -f service.yaml`

## Make sure nginx-ingress is Setup on K8s
Configure the default ingress-nginx which can be found [Here!](https://github.com/kubernetes/ingress-nginx).
This will create and setup nginx-ingress controller under ingress-nginx namespace
`kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-0.32.0/deploy/static/provider/cloud/deploy.yaml`

## Successfully exposed http container from nginx-ingress
Go to http://localhost/demo to see if accessible

### Commands
#### Get all pods in namespace
` kubectl get pods -n demo-ingress`

#### Get all Pods with more Details
`kubectl get ing -n demo-ingress -o wide --show-labels`

#### Get Http Pod Details in demo namespace
`kubectl describe pod http -n demo-ingress`

#### Get Services in demo namespace
`kubectl get svc -o wide -n demo-ingress`
