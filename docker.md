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

# Environment Variables
Python `color = os.environ.get('APP_COLOR')`  
Node `const color = process.env.APP_COLOR;`  
Ruby `color = ENV['APP_COLOR']`  
PHP `$color = getenv('APP_COLOR');`  
Go `color := os.Getenv("APP_COLOR")`  
Java `String color = System.getenv("APP_COLOR");`
