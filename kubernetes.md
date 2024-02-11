# Kubernetes command line useful
## Apply template deploy
kubectl apply -f nestjs-deployment-service.yml

## Docker build and export image to use in CI/CD pipeline
docker build -t nestjs-22 .
docker save -o nestjs-22.tar nestjs-22
sudo docker load --input nestjs-22.tar

## Listing kubernetes resources
kubectl get pods
kubectl get nodes
kubectl get deploy
kubectl get svc

kubectl scale deployment --replicas 10 nestjs-deployment
kubectl describe svc/nestjs-svc

kubectl delete svc/nestjs-svc
kubectl delete deploy/nestjs-deployment

kubectl get service --all-namespaces

kubectl delete pod nestjs-deployment-8c8ff9b4f-nnj6l

kubectl rollout restart deployment nestjs-deployment

## Dashboard
kubectl apply -f kubernetes-dashboard-deployment.yaml
kubectl -n kubernetes-dashboard apply -f admin-role.yaml
kubectl -n kubernetes-dashboard get secret admin-user-secret -o jsonpath="{.data.token}" | base64 -d


# MicroK8S Zero Ops on Ubuntu 20 LTS and UP

## Install MicroK8s on Linux

sudo snap install microk8s --classic

## Check the status while Kubernetes starts
microk8s status --wait-ready

## Turn on the services you want
microk8s enable dashboard
microk8s enable dns
microk8s enable registry
microk8s enable istio
Try microk8s enable --help for a list of available services and optional features. microk8s disable <name> turns off a service.

## Start using Kubernetes
microk8s kubectl get all --all-namespaces
If you mainly use MicroK8s you can make our kubectl the default one on your command-line with alias mkctl="microk8s kubectl". Since it is a standard upstream kubectl, you can also drive other Kubernetes clusters with it by pointing to the respective kubeconfig file via the --kubeconfig argument.

## Access the Kubernetes dashboard proxy
microk8s dashboard-proxy

## Start and stop Kubernetes to save battery
Kubernetes is a collection of system services that talk to each other all the time. If you don't need them running in the background then you will save battery by stopping them. microk8s start and microk8s stop will do the work for you.

## Access dashboard without proxy
https://garywoodfine.com/how-to-access-microk8s-dashboard-without-proxy/
microk8s kubectl -n kube-system edit service kubernetes-dashboard
 Change type in specs to NodePort
microk8s kubectl -n kube-system get services
 see port for dashboard
token=$(microk8s kubectl -n kube-system get secret | grep microk8s | cut -d " " -f1)
microk8s kubectl -n kube-system describe secret $token



## Dashboard took a lot of ram so i want to have an enpoint to extracting log from local connect to kubernetes endpoint on server
First we must test if kubernest still run ok
whether if i ran multi app with the same expose port 80 but with different cluster ip, ah must be different name space too

## Github Action
I think that we can remote connect kubernetes cluster by follow biz kubernetes engine blog
I think if we don't use dashboard, we can use Github Action with appleboy ssh action to see log
I think also we can 


## Remote Connect with VSCode
MicroK8s config file location:
cat /var/snap/microk8s/current/credentials/client.config
