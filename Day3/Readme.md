##  Launch EC2 instance
 - AMI: Ubuntu
 - Instance_Type: c7i-flex.large
 - Volume: 30 GB

## step1: Connect To Instance
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
## step2:  Install Required Plugins:
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
## step3: Tool Configuration
**SonarQube Scanner installations**
<img width="916" height="334" alt="image" src="https://github.com/user-attachments/assets/1895de3c-f906-4692-9c49-dfe393a7657d" />

**Maven installations**
<img width="904" height="267" alt="image" src="https://github.com/user-attachments/assets/a2dac6b1-13e3-41cb-9704-c0ba27221666" />

**Docker installations** --> ☑️ Install automatically
<img width="872" height="288" alt="image" src="https://github.com/user-attachments/assets/120588de-4325-4370-abf0-8838b0bf37b5" />

## step4 Run **SonarQube**
```
docker run -d --name sonar -p 9000:9000 sonarqube:lts-community
```
**connect sonarqube 
user: admin
password: admin
<img width="942" height="280" alt="image" src="https://github.com/user-attachments/assets/008a37e2-ebe6-498c-b0b0-fac3255ec556" />

---

## step5 : create token
**my account** --> **Security** --> **Tokens**

<img width="947" height="391" alt="image" src="https://github.com/user-attachments/assets/594b270e-b4b9-44af-a205-9d54cba1a011" />

## step6: Credentials
**Credentials** --> **Secret text**
**Credentials** --> Username with password

<img width="916" height="236" alt="image" src="https://github.com/user-attachments/assets/b7dd84e1-6231-4d14-bb22-da1041861327" />

## step7: system
**SonarQube servers** --> **☑️Environment variables**
<img width="896" height="380" alt="image" src="https://github.com/user-attachments/assets/d4af439e-a587-46f3-8920-6966635fc0be" />

## step8: Webhook
**administrative --> configuration --> webhook**

<img width="943" height="288" alt="image" src="https://github.com/user-attachments/assets/77f6efa6-1442-4d51-8996-ce8fb5213a1d" />

## step9: restart jenkins server
http://public-ip:8080/restart
```
sudo systemctl restart jenkins
```
## Create Pipeline
```
pipeline {
    agent any 

    tools {
        maven 'maven'
    }

    environment {
        SCANNER_HOME = tool 'sonar-scanner'
    }

    stages {

        stage('code-pull') {
            steps {
                git branch: 'main', url: 'https://github.com/sachin-rathod-tech/Project-InsureMee.git'
            }
        }

        stage('code-build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage("code-test-analysis") {
            steps {
                withSonarQubeEnv('sonar-server') {
                    sh '''
                        $SCANNER_HOME/bin/sonar-scanner \
                        -Dsonar.projectKey=InsureMe \
                        -Dsonar.projectName=InsureMe \
                        -Dsonar.sources=src \
                        -Dsonar.java.binaries=target/classes
                    '''
                }
            }
        }

        stage("code-test-quality gate") {
            steps {
                script {
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'
                }
            }
        }


        stage('code-deploy') {
            steps {
                sh 'docker build -t insure-sachin .'
                sh 'docker run -itd --name insure-me -p 8082:8081 insure-sachin'
            }
        }
    }
}
```

<img width="874" height="310" alt="image" src="https://github.com/user-attachments/assets/341ac005-9e79-4415-aff8-4b0e6316bf21" />



