`https://hub.docker.com/r/[organisation]/[image]`

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
`docker inspect [container]`  
`docker logs [container]`  

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

# Port mapping for web servers
Docker host runs containers.  
Container auto assigned IP.  
Task like web server can run on port, e.g. 5000.  
Internal IP is http://[container_ip]:[port].  
To make task public, map container IP to host IP.  
`docker run -p [host_port]:[container_port] [image]` e.g. `80:5000`  

# Volume mapping for databases / fs
Container has temp internal fs.  
To persist data, map internal fs to host fs.  
`docker run -v [container_dir]:[host_dir] [image]`, e.g. `/opt/datadir:/var/lib/my/sql`  

# Dockerfile
```
FROM Ubuntu
RUN apt-get update
RUN apt-get install -y python python-pip
RUN pip install flask
COPY app.py /opt/app.py
ENTRYPOINT FLASK_APP=/opt/app.py flask run --host=0.0.0.0
```

`docker build . -t [organisation]/[image]`  
`docker images`  
`docker run [image]`  
`docker push [organisation]/[image]`  -> push to repo  

# Environment variables
`docker run -e APP_COLOR=blue`  
`docker inspect [container]` -> Config -> Env  

Python `color = os.environ.get('APP_COLOR')`  
Node `const color = process.env.APP_COLOR;`  
Ruby `color = ENV['APP_COLOR']`  
PHP `$color = getenv('APP_COLOR');`  
Go `color := os.Getenv("APP_COLOR")`  
Java `String color = System.getenv("APP_COLOR");`  

# CMD vs ENTRYPOINT
`docker run ubuntu-sleeper sleep 10`
```
FROM Ubuntu
CMD sleep 5
```
`docker run ubuntu-sleeper 10`
```
FROM Ubuntu
ENTRYPOINT ["sleep"]
CMD ["5"] //defaults to 5 if missing
```

# Docker Compose
Version 3 deployment autocreates a network for these containers.  
`cat > docker-compose.yml`
```
version: "3"
services:
  redis:
    image: redis
  
  db:
    image: postgres:9.4
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres
  
  vote:
    image: voting-app
    ports:
      - 5000:80
  
  worker:
    image: worker-app
  
  result:
    image: result-app
    ports:
      - 5001:80
```

`docker-compose-up`

# Docker Registry
Cloud login  
`docker login private-registry.io`  
`docker run private-registry.io/apps/internal-app`  

Deploy private registry  
`docker run -d -p 5000:5000 --name registry registry:2`  
`docker image tag [image] [registry-host]:[port]/[image]`  
`docker push [registry-host]:[port]/[image]`  
`docker pull [registry-host]:[port]/[image]`  

Remove images not used by containers  
`docker image prune -a`  

# Docker Engine
Consists of Docker CLI -> REST API -> Docker Daemon.  
**Containerization**  
Namespace -> Network, Process ID, Unix Timesharing, Mount, InterProcess  
**Namespace - PID**  
The host (Linux system) runs the PID which is mapped across to a container PID.

# Docker Storage
Installing Docker on a local system creates a file system.  
Docker stores data under:  
```
/var/lib/docker
-- /aufs
-- /containers
-- /image
-- /volumes
```

## Volume mounting
`docker volume create data_volume`  
Creates `data_volume` file under `/var/lib/docker/volumes/`  

`docker run -v data_volume:/var/lib/mysql mysql`  OR  
`docker run -v /data/mysql:/var/lib/mysql mysql`  
Maps the host volume to the container local folder.  
