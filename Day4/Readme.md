# Trivy

### Follow Day 4 
https://github.com/sachin-rathod-tech/Jenkins/tree/main/Day3

#### add new step other all same 

---
## install aws cli
```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
sudo apt install unzip 
unzip awscliv2.zip
sudo ./aws/install
aws --version
```
**aws configure**
```
access-key
secret-key
region
```

## add **Plugins**
```
S3 publisher
```

## add Credentials

<img width="846" height="313" alt="image" src="https://github.com/user-attachments/assets/99b34bb9-cc2d-4e39-981b-ea5285e20ca4" />

## create s3 bucker

## new job
```
pipeline {
    agent any 

    tools {
        maven 'maven'
    }

    environment {
        SCANNER_HOME = tool 'sonar-scanner'
        S3_BUCKET = "ssrajamoli-s3"
        REGION = "eu-west-3"
        warFile = "target/Insurance-0.0.1-SNAPSHOT.jar"
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
        
        stage('code-push'){
            steps{
                withCredentials([aws(accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'aws-cred', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY')]) {
                   sh 'aws s3 cp ${warFile} s3://${S3_BUCKET}/Artifacts/ --region ${REGION}'
                 }
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
        stage('docker-image'){
            steps{
                sh 'docker build -t rathodsr/insure-b8:v5 .'
            }
        }
        stage('image-push') {
            steps {
       	       withCredentials([usernamePassword(credentialsId: 'docker-cred', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
            	sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                sh 'docker push rathodsr/insure-b8:v5'
               }
            }
        } 
        stage('code-deploy'){
            steps{
                sh 'docker run -itd --name scareface -p 8082:8081 rathodsr/insure-b8:v5'
            }
        }
    }
}
```


<img width="959" height="418" alt="image" src="https://github.com/user-attachments/assets/a5a935c8-8285-44c7-8444-cce10b1f06ca" />

