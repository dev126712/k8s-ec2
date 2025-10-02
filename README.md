# Kubernetes demo



## On Debian Ec2 instance 'User data'.
### - The bash script first update the packeages, install git. 
### - Then clone my other github repo that insatll Docker, Terraform (even though you dont need it for this demo), Kubernetes (kubectl & Minikube) and AWS cli. 
### - After that it clone this repo that contain the Kubernetes demo, install npm and express.
### - Give the permission needed to use docker without the 'sudo'. You might need the do it manually on the instance.
### - Install jq that format the JSON return by kubernetes.
### - Build the Docker image.
#### Even though your instance is up and running it should take a couple of minute to install everything so be patient :).
#### If you're not using user data you can still run this on a bash script on your machine.
``` bash
#!/bin/bash

sudo apt update
sudo apt upgrade -y
sudo apt install git -y
git clone https://github.com/dev126712/Installation.git
cd Installation
chmod +x 'DockerTerrKub.sh'
./'DockerTerrKub.sh'
cd ../home/admin
git clone https://github.com/dev126712/project.git
cd project/node-app-kubernetes
sudo apt install npm -y
npm install express
sudo usermod -aG docker $USER && newgrp docker
sudo apt install jq -y
sudo docker compose up --build
```

### After everything installed make sure that the docker container is running by rinning this command:

``` bash
docker ps
```
### If its says that you dont have the permission needed run this command that gonna give your user the permission to run docker command without 'sudo':

``` bash
sudo usermod -aG docker $USER && newgrp docker
```
### Then you can start minikube by running:

``` bash
minikube start
```
### After that you can run this command and you can see that minikube is running a control plain:

``` bash
kubectl get nodes
```

### To check if the cluster is running you can run:

``` bash
kubectl cluster-info
```

## Deplyment

### Now deploy the kubernetes files by running each one individualy:

``` bash
kubectl apply -f k8s/deployment.yml
kubectl apply -f k8s/service.yml
```
### Or

``` bash
kubectl apply -f k8s/
```

### To check the pod status you can run :

``` bash
kubectl get pods -w
```
## To get access to the services run:

``` bash
kubectl get services
```

## Test

### With the help of minikube you can access your services by running:

``` bash
minikube service ...






























