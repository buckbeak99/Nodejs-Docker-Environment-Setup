# Nodejs-Docker-Environment-Setup
## Nodejs setup: 
### For Linux(Ubuntu) 
***Step 1:*** Add NodeSource PPA  
a. Update the Apt index  
```bash
sudo apt update
```   
b. Go to the home directory and run this command on the terminal. If you don’t have curl then install it.  
```bash
cd ~
```  
```bash
curl -sL https://deb.nodesource.com/setup_14.x -o setup_14.sh
```  
c. If you don’t have curl then install using this command.
```bash
sudo apt install curl
```   
d. Next, let's run the setup which will add the NodeSource PPA: 
```bash
sudo sh ./setup_14.sh
```   

***Step 2:*** Install Nodejs  
e. We will now have the NodeSource PPA added, allowing us to install NodeJS 14. First let's update the APT package library:  
```bash
sudo apt update
```  
```bash
sudo apt install nodejs
```  
***Step 3:*** Check the node version  
```bash
node --version
```  
```bash
npm --version
```  

## Docker Setup  
The first step is to set up the computer for Hyperledger Fabric.  
1. Install cURL - a command line tool to access web protocols in command line:  
```bash
sudo apt-get install curl:
```  
2. Next, we will install Docker and Docker Compose using the following steps.  
a. Remove the older versions of Docker (if any) using the following commands:  
```bash
sudo apt-get remove docker docker-engine docker.io containerd run
```   
It is okay if the above command reports that none of these packages is installed   
b. Update apt: 
```bash
sudo apt-get update
```  
c. Install packages to allow apt to use a repository over HTTPS:  
```bash
sudo apt-get install apt-transport-https ca-certificates gnupg-agent software-propertiescommon
```  
d. Add Docker’s official GPG key:  
```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - 
```  
e. Use the following command to set up the stable repository. Please combine them in the same line while executing this command.  
```bash
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```  
f. Update the apt package again: 
```bash
sudo apt-get update
```  
g. Install docker: 
```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io
```  
h. Test docker installation: 
```bash
docker run hello-world
```  
If it shows a message like "Hello from Docker" -> Then docker is fully installed  
i. If you cannot run the above command and it shows the permission denied message, then you might need to use the following commands to ensure that the user can run the docker commands without being sudo:  
```bash
sudo groupadd docker
``` 
(it might report that the docker group is already added, it is fine)  
ii. (adding current user to the docker group, any command will do) 
```bash
sudo usermod -aG docker $USER / sudo gpasswd -a $USER docker
```  
iii. (to activate the change)
```bash 
newgrp docker
``` 
iv. 
```bash 
docker run hello-world
``` 
If it shows a message like "Hello from Docker" -> Then docker is fully installed  

3) Next, we will install docker-compose using the following steps. Docker Compose makes it easier for users to streamline the docker containers management processes, including starting up, shutting down, and setting up intra-container linking and volumes.   
a. Download the docker-componse binary file from this location: go to https://docs.docker.com/compose/install/ for latest version of docker compose
```bash
 sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```   
b. Make it executable: 
```bash
sudo chmod +x /usr/local/bin/docker-compose
```  
c. Check the installation: 
```bash
docker-compose –version
``` 
If it shows an output with a version, the docker-compose is properly installed.   
d. Now, test the installation using the following steps:  
i. 
```bash
mkdir hello-world
```  
ii. 
```bash
cd hello-world
```   
iii. 
```bash
nano docker-compose.yml
``` 
(short form of YAML, Ain't Markup Language)   
iv. Add the following contents:   
```bash
docker-compose up 
```  
The first time we run the command, if there's no local image named hello-world, Docker Compose will pull it from the Docker Hub public repository. Then it prints a similar message like the hello-world docker we tested previously. This indicates our docker-compose installation is complete.  
e. Next, we will go through some commands to handle docker/docker-compose.   
i. to look at the docker images in our computer
```bash
docker images
```    
ii. it lists the active docker containers. Use the option ‘a’ (```$ docker ps -a```) to list all containers, both the active as well as inactive Containers.
```bash
docker ps
```      
iii. To shut down a single container: 
```bash
docker rm container_numer
``` 
(container_number from docker ps -a command)    
iv. To shut down all containers: 
```bash
docker rm $(docker ps -a -f status=exited -q)
```   
v. Removing an image from the computer: 
```bash
docker rmi hello-world
``` 
or 
```bash
docker rmi fe0775514017
``` 
(number from docker ps -a command)  
vi. To remove all containers: 
```bash
docker rmi -f $(docker images -a -q)
```   
### Go Lang Setup: 
a. Go to: https://golang.org/dl/. Then click for the Linux tar file. Once clicked, a popup will appear, select Save.   
b. The file will be downloaded in ~/Downloads. cd into ~/Downloads in the command prompt and then issue the following command: 
```bash
sudo tar -C /usr/local -xzf go1.11.5.linux-amd64.tar.gz
```     
c. Examine if the following structure has been created: /usr/local/go. If it does not match it like this, see what directory structure it has created. You need to locate the directory called "go" under which api, bin and other directories need to reside. Note the directory path containing the "go" directory. 
d. Add the "go" directory in the PATH variable. To do this, use the following commands:   
i. 
```bash
cd
```   
ii. 
```bash
nano .profile
```   
iii. Add this line at the end of your profile: 
```bash
export PATH=$PATH:/path_to_go/bin
```   
iv. Save by using: $ crtl+o and then $ crtl+x   
v. 
```bash
source .profile
```   
vi. Check if the proper go path is printed in the console: 
```bash
echo $PATH
```   
e. Add GOPATH variable into your path:   
i. 
```bash 
cd
```   
ii. 
```bash
mkdir -p go/src
```   
iii. 
```bash
mkdir -p go/bin
```   
iv. 
```bash
cd
```   
v. 
```bash
nano .bashrc
```  
vi. Add: 
```bash
export GOPATH=$HOME/go
```   
vii. Add: 
```bash
 export PATH=$PATH:$GOPATH/bin
 ```   
viii. $ crtl+o and then $ crtl+x to save and exit   
ix. 
```bash
source .bashrc
```  
x. Check if the proper GOPATH is printed in the console: 
```bash
echo $GOPATH
```   
xi. Check if bin under GOPATH is in the path: 
```bash
echo $PATH
```   
f. Test your go installation:   
i.  
```bash
cd go/src 
```   
ii. 
``` bash 
mkdir hello
``` 
iii. 
```bash
cd hello
``` 
iv.
```bash 
touch hello.go
``` 
v. 
```bash
nano hello.go
``` 
vi. Paste the following contents: write some go functions   
vii. $ crtl+o and then $ crtl+x to save and exit  
viii. While in ~/go/src/hello: $ go build   
ix. Use this command: $ ./hello   
If it prints hello world, then your go installation is fine Now your work environment is fully set up.   

*** Thank You ***
