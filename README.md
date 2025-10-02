# Kubernetes demo



## On Debian Ec2 instance 'User data'.
### - The bash script first update the packeages and install git. 
### - Then clone my other github repo that insatll Docker, Terraform (even though you dont need it for this demo), Kubernetes (kubectl & Minikube) and AWS cli. [GitHub Pages](https://github.com/dev126712/Installation.git) 
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
### If its says that you dont have the permission needed. You need to manually run this command that gonna give your current user the permission needed  to run docker command without 'sudo

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
#### Make sure to be in the 'node-app-kubernetes' folder.
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

### With the help of minikube you can access your services by running in myy case 'devops-k8s-api-service':

``` bash
minikube service devops-k8s-api-service
```

## Error

### You might get this error wich is normal because we are running minikube on an ec2 instance instead of our local machine and there no browser.
![alt text](https://github.com/dev126712/k8s-ec2/blob/27e6584daa91c4763d787148c9582ea9c24afbed/Images/Screenshot%202025-10-02%204.21.35%20PM.png)

### Hopefully we can still access it by using the command curl that fetch HTML pages and jq that format the JSON we receive.

### Exemple:
``` bash
curl -s http://192.168.49.2:32036 | jq .
```

### You should get something like this: 
![alt text](https://github.com/dev126712/k8s-ec2/blob/27e6584daa91c4763d787148c9582ea9c24afbed/Images/Screenshot%202025-10-02%204.21.54%20PM.png)

### As expected if you look closely to the pod field you can see that there 2 different pod id:

#### First:
![alt text](https://github.com/dev126712/k8s-ec2/blob/7c8fe6502a41491f89df1460e560bfec883d656c/Images/Screenshot%202025-10-02%204.30.40%20PM.png)

#### Second
![alt text](https://github.com/dev126712/k8s-ec2/blob/7c8fe6502a41491f89df1460e560bfec883d656c/Images/Screenshot%202025-10-02%204.31.01%20PM.png)

### That because in the 'deployment.yml' file we specified 2 replicas.
![alt text](https://github.com/dev126712/k8s-ec2/blob/4ea53f08db8700c548e22d80f8fead779e5c895c/Images/Screenshot%202025-10-02%204.35.55%20PM.png)






























