# Docker Installations and Docker comamnds 
1)  Docker installation 
2)  Container Deployment 
3)  Image creation 
4)  Volume management
5) Docker networking 

Docker Installtion for Ubuntu 
- Update the ubuntu repository 
- Use the apt command to install the docker.io package:
```
sudo apt update
```
```
sudo apt install docker.io
```
- Start the docker and enable it to start after the system reboot:
```
sudo systemctl start docker
```
```
sudo systemctl enable docker
```
```
sudo systemctl status docker
```
- View the Docker version 
```
docker --version
```
Download a new Docker image
```
docker pull httpd 
```
Download the Docker image with Specific version 
 
 docker pull httpd:2.4.52
 
To list the docker images on the system with:

docker images


docker inspect image <image name>

To run a container based on an existing Docker image, use the command:

docker run –name myapp -d httpd
```
To list all the running Container 

docker ps

List all the docker containers (running/exited/stopped) 
docker ps –a

Start,Pause,Unpause,restart,Stop the Docker container
docker start myapp01 
docker pause myapp01
docker unpause myapp01
docker restart myapp01 
docker stop myapp01 

$docker rm <CONTAINER ID> -->How to remove or delete Docker Images?
$docker rmi <Image name>  -->How to remove the Docker Image?


Port Forwarding
$docker run -p 8080:80 -d --name myweb httpd 
$docker exec -it myweb bash -->login to container


## Images and Their Layers: Discover the Image Cache

docker image ls
docker history httpd:latest
docker history httpd
docker image inspect httpd
