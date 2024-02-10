kubectl apply -f nestjs-deployment-service.yml

docker build -t nestjs-22 .
docker save -o nestjs-22.tar nestjs-22
sudo docker load --input nestjs-22.tar


kubectl get pods
kubectl get nodes
kubectl get deploy
kubectl get svc

kubectl scale deployment --replicas 10 nestjs-deployment
kubectl describe svc/nestjs-svc

kubectl delete svc/nestjs-svc
kubectl delete deploy/nestjs-deployment


### See IP of all cluster
kubectl get service --all-namespaces

kubectl delete pod nestjs-deployment-8c8ff9b4f-nnj6l

kubectl rollout restart deployment nestjs-deployment
