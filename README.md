# Docker Installations and Docker comamnds 
- Docker installation 
- Container Deployment 
- Image creation 
- Volume management
- Docker networking 

Update the ubuntu repository 
```
sudo apt update
```
Use the apt command to install the docker.io package:
```
sudo apt install docker.io
```
Start docker and enable it to start after the system reboot:
** Start the Docker service 
```
sudo systemctl start docker
```
Enable the Docker Service 
```
sudo systemctl enable docker
```
Check the Docker Status
```
sudo systemctl status docker
```
View the Docker version 
```
docker --version
