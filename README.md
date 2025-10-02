# Kubernetes demo



## On Debian Ec2 instance 'User data'.
### The bash script first update the packeages, install git. 
### Then clone my other github repo that insatll Docker, Terraform(even though you dont need it for this demo), Kubernetes(kubectl & Minikube) and AWS cli. 
### After that it clone this repo that contain the Kubernetes demo, install npm and express.
### Give the permission needed to use docker without the 'sudo'. You might need the do it manually on the instance.
### Build the Docker image.
### Install jq that format the JSON return by kubernetes.

``` bash
#!/bin/bash

sudo apt update
sudo apt upgrade -y
sudo apt install git -y
git clone https://github.com/dev126712/Installation.git
cd ../home/admin
https://github.com/dev126712/k8s-ec2.git
cd k8s-ec2/node-app-kubernetes
sudo apt install npm -y
npm install express
sudo usermod -aG docker $USER && newgrp docker
sudo docker compose up --build
sudo apt install jq -y

```

