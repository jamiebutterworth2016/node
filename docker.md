Image tags can be specified with `[image]:[tag]`.
`docker run` dl image first, then run in container.  
Container runs a task (NOT an OS) and exits.

`docker images`  
`docker rmi [image]`  
`docker pull [image]` -> dl image without running  
`docker run [image]` -> attach to console  
`docker run -d [image]` -> run in background, detached from console  
`docker run -it [image]` -> run in interactive terminal mode, allows for input (stdin)  

`docker ps -a` -> ls containers  
`docker stop [container]`  
`docker rm [container]`  
`docker exec [container] cat /etc/hosts` -> execute command on running container
`docker attach [container_id]` -> attach running container to console  


# Get started
Ubuntu
```
sudo -i
apt-get remove docker docker-engine docker.io containerd runc
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh
docker version
docker run -it centos bash
```
