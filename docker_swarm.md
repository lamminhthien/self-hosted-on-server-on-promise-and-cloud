docker build -t nestjs-22 .
<!-- docker save -o nestjs-22.tar nestjs-22 -->
<!-- sudo docker load --input nestjs-22.tar -->
docker swarm init
docker stack deploy --compose-file docker-compose-ssh.yml app
docker service ls
docker service rm app_app
docker service update --force app_app
