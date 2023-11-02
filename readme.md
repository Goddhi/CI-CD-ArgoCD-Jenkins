Steps involved in this project 

Install Sonarqube Using Docker and Docker Compose
https://blog.devops.dev/install-sonarqube-server-on-ubuntu-using-docker-compose-f7b168492649

Install Jenkins
Clone this repo
https://github.com/Goddhi/CI-CD-AgroCD-Jenkins.git

configure the Jenkins pipeline in Jenkins

install the following plugins 
Docker Pipeline
Sonar Scanner

## To connect Jenkins and Sonarqube
Generate a token from Sonarqube and paste the token in jenkins credentials 


## Grant Jenkins user and Ubuntu user permission to docker deamon.
sudo su - 
usermod -aG docker jenkins
usermod -aG docker ubuntu
systemctl restart docker


## Grant permission to  all user to use docker demon
sudo chmod 777 /var/run/docker.sock


## Installing AgroCD using Operator..
Benefits of using operator is to get telementary on about the controller(AgroCD)