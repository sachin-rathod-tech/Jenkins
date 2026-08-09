##  Launch EC2 instance
 - AMI: Ubuntu
 - Instance_Type: c7i-flex.large
 - Volume: 30 GB

##  Connect To Instance
 - Install java
 - Install Jenkins
 - Install Docker
 - Install maven
 - Install SonarQube    # used for code quality testing

**java**
```sudo apt update
sudo apt install fontconfig openjdk-21-jre
java -version
```   
**Jenkins**
````
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2026.key
echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
````

**maven**
```
sudo apt install maven -y
```
**docker**
```
sudo apt install docker.io -y
sudo systemctl start docker
sudo usermod -aG docker jenkins
sudo usermod -aG docker ubuntu
newgrp docker
sudo chmod 777 /var/run/docker.sock
```
##  Connect to Jenkins 
```
public-ip:8080
```
##  Install Required Plugins:
   **Install below plugins**

````
Amazon ECR
````
````
SonarQube Scanner
````
````
docker All
````
````
stage view
````
```
maven
```

