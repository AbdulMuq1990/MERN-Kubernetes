Create a .env file in backend folder, this repo doesnt have


------- Create an EC2 t2-medium instance with below userdata & ports in security group ------

#!/bin/bash


#Install Mongodb & Mongosh shell
sudo apt update 
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs

sudo wget https://repo.mongodb.org/apt/ubuntu/dists/jammy/mongodb-org/7.0/multiverse/binary-amd64/mongodb-org-server_7.0.5_amd64.deb

sudo dpkg -i mongodb-org-server_7.0.5_amd64.deb
sudo systemctl status mongod
sudo systemctl start mongod

sudo wget https://downloads.mongodb.com/compass/mongodb-mongosh_2.1.1_amd64.deb
sudo dpkg -i mongodb-mongosh_2.1.1_amd64.deb

#Install Docker
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg -y
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
sudo apt-get install docker-compose -y
sudo usermod -aG docker ubuntu
sudo chown ubuntu:docker /var/run/docker.sock
sudo systemctl start docker

-----------------------------------------------------------------------------------------------
Ports to be opened in Security Group
22 ssh						custom tcp 3001
80 http	(for nginx)				custom 3333		(For nginx mapped from 80)
Custom tcp 5000 (for Nodejs)			custom tcp 27017	(For mongo DB)
Custom tcp 3000 ()				

---------------------------------------------------------------------------------------------------------
Login to MONGODB Atlas https://cloud.mongodb.com/v2/65adf6b57077165110fabeb5#/security/network/accessList 


dashboard--> click on Network Access --> click Add IP Address
Take Public IP of EC2 Instance and Add it here 

------------------------------------------------------------------------------------------------------
Clone source code (Create a apps directory in root directory)

cd /

mkdir apps

cd apps/

App/# git clone https://github.com/AbdulMuq1990/MERN-Docker.git

