# Kubernetes Workshop

We are going to deploy and expose to the world 3 applications using Digitalocean. The dashboard will help us to see what is happening in the nodes. Also, we are going to see the self-healing in action. Happy k8s

## Steps

### Create a new cluster

Digital Ocean cluster with 3 nodes

### Configure the k8s client

`export KUBECONFIG=~/Desktop/k8s-kubeconfig.yaml`

`kubectl get nodes`

### Deploy kuard

`kubectl apply -f kuard/deployment.yaml`

`kubectl apply -f kuard/service.yaml`

### Deploy nginx

`kubectl apply -f nginx/deployment.yaml`

`kubectl apply -f nginx/service.yaml`

See the Digitalocean Load Balancer in Networking

### kube-ops-view dashboard

`git clone https://github.com/hjacobs/kube-ops-view`

`kubectl apply -f kube-ops-view/deploy/`

`kubectl get pods`

### Expose the kube-ops-view dashboard

Edit the type in service.yaml (`type: LoadBalancer`)

location kube-ops-view/deploy/service.yaml

`kubectl apply -f kube-ops-view/deploy/`

### Scale up the applications

Edit all the deployment.yaml files and then apply the changes

Kuard deployment.yaml `replicas: 10`

`kubectl apply -f kuard/deployment.yaml`

Dashboard deployment.yaml `replicas: 5`

Nginx deployment.yaml `replicas: 10`

### Scale down an application

Review the steps above

Nginx deployment.yaml `replicas: 5`

### Remove a pod

`kubectl get pods`

`kubectl delete pod <pod-name>`

### Remove all the kuard pods

`kubectl delete $(kubectl get pods --selector=app=kuard -o name)`

### Remove a droplet in DigitalOcean UI

See the self healing in the dashboard

See the creation of the new droplet in Digitalocean

### Remove the objects in the cluster

**notice:** If you don't remove load balancer and droplets you will have some charges

`kubectl delete  -f nginx/ -f kuard/ -f kube-ops-view/deploy/`

## Common commands

```
kubectl get pods
kubectl get services
kubectl get nodes
kubectl get deployments
kubectl delete pod <name>
```
