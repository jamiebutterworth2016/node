`docker images` -> ls images  
`docker rmi [image]` -> rm image  
`docker pull [image]` -> dl image  
`docker run [image]` -> dl and run image in container, attached to console. Container runs a task (NOT an OS) and exits.  
`docker run -d [image]` dl and run image in container, detached from console

`docker ps -a` -> ls containers  
`docker stop [container]`  
`docker rm [container]`  
`docker exec [container] cat /etc/hosts` -> execute command on running container
`docker attach [container_id]` -> attach running container to console  


# Get started
Ubuntu
```
sudo apt-get remove docker docker-engine docker.io containerd runc
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo docker version
```
