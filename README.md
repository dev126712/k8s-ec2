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
cd project
sudo apt install npm -y
npm install express
