## Docker Training 

1) Docker Installation 
2) Container Deployment 
3) Image creation 
4) Volume managment 
5) Basic Docker networking  

- Docker Installation

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
docker version

docker info

docker

docker container run

docker run
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
# Image Creation 

Steps 

	• OS - Ubuntu
	• Update apt repo
	• Install dependencies using apt
	• Install python dependencies using pip
	• Copy source code to /opt folder
	• Run the web using flask command 
	
Minaly two feilds are aviable Instruction &  Arguement 

<img width="308" alt="image" src="https://user-images.githubusercontent.com/62458394/154254272-559bc548-b7ef-45ed-aa56-c359404a727c.png">

