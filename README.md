# Jenkins Docker file with Terraform, Ansible, AWS CLI and Google authenticator. 
Jenkins is an important DevOps tool used to do continous integration (CI) and continous deployment (CD) of project. Together, both CI and CD create a full CI/CD pipeline, which can speed up the application building and exapnding process. 

In this directory I put two files - a docker file and a docker-compose file. They can be used a base template for using Jenkins. 
The docker file includes Jenkins along important DevOps softwares - 
* Terraform - A software used for provisioning and shaping cloud architectures, by text commands. 
* Ansible - an application used to configure servers, by SSH connecting to them and performing commands remotely. Example for such commands can be secure copy (```scp``` in bash terminal) , shell commands etc... 
* AWS CLI - which stand for Amazon web services command line interface. This can be configured in order to access AWS and configure it from the Terminal. 
* G authentication - used to connect to Google Cloud Platform (GCP) , and allows connection from the local computer. For example, it allows to push docker images from the local machine to the Google Container Registry (GCR) which is a google cloud service used to store docker images. 
* Nano - I also installed nano terminal text editor, so it can be easier to debug and configure the Jenkins image. 

If this are installed on Jenkins, you can use Jenkins in order to connect to cloud providers and to configure your cloud architecture. This will allow to make full automatation of the continous deploymnet (CD) which is a parts of the CI/CD pipeline! 


## To run the docker file - 
cd from your terminal to the directory with the files, then run the docker-compose file - 
```bash 
docker-compose up
docker-compose up --build #If you changed the images, then you need to rebuild it. BY default docker-compose doesn't rebuild the image unless you mention it by adding --build argument. 
```

If you want to run the docker file itself, without docker compose - 
```bash
docker run -v /var/run/docker.sock:/var/run/docker.sock -v jenkins_data:/var/jenkins_home -p 801:8080 my-jenkins-image #If the Dockerfile is in the local directory. 
```bash
docker container ls #Find you Jenkins container name
docker log <containername> # Get logs from the container. 
docker exec -it <containername> bash #This will open a bash session in the Jenkins container. 
```

### To debug the container - 
You can connect to it with a bash session. As mentioned, I installed Nano text editor so you can read and edit files more easy if need to. 


## Pre-requisites install docker and docker-compose - 
In order to run the docker file itself, docker needs to be installed on your local machine. To install docker on use these commands - 
```bash
#This script will install docker on the local machine. 

#Update apt-get and do pre-configurations. 
sudo apt update
sudo apt install apt-transport-https ca-certificates curl software-properties-common


#Add docker repository and install docker. 
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
sudo apt update
apt-cache policy docker-ce
sudo apt install docker-ce


#Test
echo "docker is installed. " 
sudo systemctl status docker
```

To use docker-compose, install it by running these commands - 
```bash
#Install docker-compose
sudo curl -L "https://github.com/docker/compose/releases/download/1.25.3/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

#Optional - add auto-completion. ( This is not a must, though might be useful... ) 
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose


#Test
echo "finished installing docker-compose"
docker-compose --version 
```