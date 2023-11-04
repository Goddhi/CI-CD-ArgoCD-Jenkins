## Deplyoed Java Applicaton into Kubernetes Cluster


### CI Implemented using Jenkins
### CD Implemented using ArgoCD

The CI involves utilizing Jenkins to create a CI pipeline that build, test (Maven), analyzes code for code smells(sonarqube), build and push image to DockerHub and then update the deploymentcode.

The CD involves Utilizing argoCD to dynamically deploy the application into kubernetes cluster

## Benefit of using the ArgoCd 
Ability to visualize deployment issues, detect and remediate configuration drift.
Verify changes to deoployment file and rollback changes

## Steps involved in this project 

### Install Sonarqube Using Docker and Docker Compose on VM1
https://blog.devops.dev/install-sonarqube-server-on-ubuntu-using-docker-compose-f7b168492649

### Install Jenkins on VM1
https://www.jenkins.io/doc/book/installing/

### Clone this repo
https://github.com/Goddhi/CI-CD-AgroCD-Jenkins.git

### configure the Jenkins pipeline in Jenkins

install the following plugins 
Docker Pipeline
Sonar Scanner
Pipeline script is written in this file /CI-CD-AgroCD-Jenkins/Jenkins-Zero-To-Hero/java-maven-sonar-argocd-helm-k8s/spring-boot-app/Jenkinsfile
## To connect Jenkins and Sonarqube
Generate a token from Sonarqube and paste the token in jenkins credentials 


## Grant Jenkins user and Ubuntu user permission to docker deamon.
sudo su - 
usermod -aG docker jenkins
usermod -aG docker ubuntu
systemctl restart docker


## Grant permission to  all users to use docker daemon
sudo chmod 777 /var/run/docker.sock


## Push code to github and run build on the pipeline so all stages get passed and the docker image is pushed to DockerHub.

### CD implementation starts here 

## Install Minikube 
[https://minikube.sigs.k8s.io/docs/start/]

## cmd to start minikube
`minikube start`

## Install AgroCD on Minikube K8Scluster
[https://medium.com/@nanditasahu031/getting-started-with-argocd-b5a02353e144]


## Possibe Error during installation of ArgoCD 'imagepullbackoff' 
This is as a result of Insufficient disk space...
fix issue by expanding the VM disk

### Port Forward so we can Access  ArgoCD UI in the browser
kubectl port-forward --address 0.0.0.0 svc/argocd-server -n argocd 8080:443
remember to create a service an inbound rule of port 8080

`https://"public-ip":8080`


## Login
Default Username: admin
### Get password using the command below
`kubectl get secret agrocd-initial-admin-secret -n argocd -o yaml`

## convert the plain text password to base64 using the command below
echo "plain-text-password" | base64 -d

### Follow the necessary steps in the picture below to deploy the application into k8s cluster using ArgoCD

![first image](/home/goddhi/Downloads/CI-CD-ArgoCD-Jenkins/image1.png)
![first image](/home/goddhi/Downloads/CI-CD-ArgoCD-Jenkins/image2.png)
![first image](/home/goddhi/Downloads/CI-CD-ArgoCD-Jenkins/image3.png)


### Verify that application has been deployed to K8s
`kubectl get pods -n argcocd`

![first image](/home/goddhi/Downloads/CI-CD-ArgoCD-Jenkins/image4.png)



