# Docker Administration Deep Dive

# Before start this excercise,you must have running Ubuntu linux machine.
- Create one VM
 - Create 1 Ubuntu linux machine in AZURE Cloud [or] AWS Cloud [or] In your local laptop using Vmware or oracle virtual box or hyper-v  workstation
 - Make sure you opened SSH,http,8080 ports for this new VM
# Topics 
1) Docker Installation 
2) Container Deployment 
3) Image creation 
4) Volume managment 
5) Basic Docker networking  

# Docker Installation

Update the ubuntu repository 

```
sudo apt update
```
Use the apt command to install the docker.io package:
```
sudo apt install docker.io
```
Start docker service and enable it to start after the system reboot:
```
sudo systemctl start docker
```
```
sudo systemctl enable docker
```
```
sudo systemctl status docker
```
Check Our Docker Install and Config
```
docker --version
docker version
docker info
```


# Container Deployment
- Download a new Docker image
```
docker pull httpd 
docker pull httpd:2.4.52  #Specify the version  
```
- To list the docker images on the system with:
```
docker images
docker inspect image <image name>
docker history httpd
```
- To run a container based on an existing Docker image, use the command:
```
docker run –name myapp -d httpd 
```
- To list the running Container
```
docker ps 
```
- List all the docker containers (running/exited/stopped) 
```
docker ps –a
```
- Start,Pause,Unpause,restart,Stop the Docker container
```
docker start myapp01 
docker pause myapp01
docker unpause myapp01
docker restart myapp01 
docker stop myapp01 
```
- Port Forwarding
```
docker run -p 8080:80 -d --name myweb httpd 
```
- how to login the Docker container
```
docker exec -it myweb bash
```
- How to remove or delete Docker Container?
```
docker rm <CONTAINER ID>
```
How to remove the Docker Image?
```
docker rmi docker rmi <Image name>
```
# Docker build

The specific commands you can use in a dockerfile are:

FROM, PULL, RUN, and CMD

- FROM - Creates a layer from the ubuntu:18.04
- PULL - Adds files from your Docker repository
- RUN - Builds your container
- CMD - Specifies what command to run within the container

Steps 
1)  Create a file named Dockerfile
2)  Add instrction in Dockerfile
3)  Build dockerfil to create image
4)  Run image to create container

- Example 01	  
```	  
FROM ubuntu
MAINTAINER shyju
RUN apt-get update
CMD ["echo", "Hello World ......! My frist Docker image"]
```
```
docker build -t myimage:1.0 .
```
- Example 02 
```
FROM ubuntu:latest
RUN apt update
RUN apt install -y nginx
ADD index.html /usr/share/nginx/html/index.html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```
```
docker build -t myimage02 .
```
# Volume managment
- By default all files created inside a container are stored on a writable container layer
- tmpfs mounts: A tmpfs mount is not persisted on disk, either on the Docker host or within a container. It can be used by a container during the lifetime of the container, to store non-persistent state or sensitive information
- Volumes: Created and managed by Docker. You can create a volume explicitly using the docker volume create command, or Docker can create a volume during container or service creation.
When you create a volume, it is stored within a directory on the Docker host. When you mount the volume into a container, this directory is what is mounted into the container
- Bind mounts:  Bind mounts have limited functionality compared to volumes. When you use a bind mount, a file or directory on the host machine is mounted into a container. The file or directory is referenced by its full path on the host machine.

<img width="373" alt="image" src="https://user-images.githubusercontent.com/62458394/154840921-561e7f03-0a44-4a98-a585-0355e2340c8d.png">


craete the Volume 
```
 docker volume create my-vol
 ```
 List volumes:
 ```
 docker volume ls
 ```
 Inspect a volume:
 ```
 docker volume inspect my-vol
 ```
 Remove a volume:
 ```
 docker volume rm my-vol
 ```
 - Attach a volume to container 
 ```
 docker run -d --name myvm01 --mount source=myvol,destination=/data httpd
 ```
 ```
docker stop myvm01
```
```
docker rm myvm01
````
 
 - Bind Mounts Example 
 ```
 docker run -d --name myvm01 -v /data:/data httpd 
 ```
 
 https://docs.docker.com/storage/
 
 # Docker Networking 
 
 
 <img width="601" alt="image" src="https://user-images.githubusercontent.com/62458394/154846680-202fd3a1-ad79-4d1b-aaab-9ae8a780d16d.png">
 
 - bridge: The default network driver. If you don’t specify a driver, this is the type of network you are creating.
- host: For standalone containers, remove network isolation between the container and the Docker host, and use the host’s networking directly
- none: For this container, disable all networking. Usually used in conjunction with a custom network driver

--> Docker network Architecture  Publishing port 80 to 8080


<img width="535" alt="image" src="https://user-images.githubusercontent.com/62458394/154848524-1c507fbd-0222-4a46-bb4f-303a532a5fdb.png">
```
docker network ls

- Create a user defined bridge network 
```
docker network create my-net

```
```
docker network ls
```
```
docker inspect network my-net
```
```
docker network rm my-net
```
```
docker network create --driver=bridge --subnet=192.168.0.0/16 my-net
```
```
docker inspect network my-net
```
- create a container with defined bridge network 

```
 docker run -d --network my-net --name vm01 httpd
``` 
```
docker inspect vm01
```
```
 docker exec -it vm01 bash 
```



