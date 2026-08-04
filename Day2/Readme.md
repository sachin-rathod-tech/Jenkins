# Jenkins Day 2 - Jenkins Pipeline

## Objective

Learn how to create a basic Jenkins Pipeline that automates code pull, build, and deployment.

---

# What is a Jenkins Pipeline?

A **Jenkins Pipeline** is a collection of stages that automates the software delivery process.

> **Definition:** A Jenkins Pipeline is a CI/CD workflow written as code using a `Jenkinsfile`.

---

# Why Use a Pipeline?

- Automates the CI/CD process
- Reduces manual work
- Easy to maintain
- Faster software delivery
- Pipeline as Code

---

# Pipeline Workflow

```
GitHub
   │
   ▼
Code Pull
   │
   ▼
Build
   │
   ▼
Deploy
```

---

# Jenkinsfile

```groovy
pipeline {
    agent any

    stages {

        stage('Code Pull') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Alpesh-Rajendra/Project-InsureMe.git'
            }
        }

        stage('Code Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Code Deploy') {
            steps {
                sh 'docker build -t my-pipeline .'
                sh 'docker run -itd --name my-cont -p 8081:8081 my-pipeline'
            }
        }
    }
}
```

---

# Pipeline Stages

## Stage 1 - Code Pull

Pulls the latest source code from the GitHub repository.

```groovy
git branch: 'main',
    url: 'https://github.com/Alpesh-Rajendra/Project-InsureMe.git'
```

---

## Stage 2 - Code Build

Builds the project using Maven.

```groovy
sh 'mvn clean package'
```

---

## Stage 3 - Code Deploy

Builds the Docker image.

```groovy
sh 'docker build -t my-pipeline-05 .'
```

Runs the Docker container.

```groovy
sh 'docker run -itd --name cont5 -p 8082:8081 my-pipeline-05'
```

---

# Keywords

## pipeline

Defines the Jenkins Pipeline.

## agent any

Runs the pipeline on any available Jenkins agent.

## stages

Groups all pipeline stages.

## stage

Represents one step in the CI/CD process.

## steps

Contains the commands executed in a stage.

## sh

Executes Linux shell commands.

---

# Pipeline Flow

```
Developer
      │
      ▼
GitHub Repository
      │
      ▼
Jenkins Pipeline
      │
      ▼
Code Pull
      │
      ▼
Maven Build
      │
      ▼
Docker Build
      │
      ▼
Docker Container
```

---

# Prerequisites

- Java Installed
- Maven Installed
- Docker Installed
- Jenkins Installed
- Git Installed
- GitHub Repository
- Jenkins has permission to run Docker

---

# Useful Commands

Check Maven

```bash
mvn --version
```

Check Docker

```bash
docker --version
```

List Docker Images

```bash
docker images
```

List Running Containers

```bash
docker ps
```

Stop Container

```bash
docker stop cont5
```

Remove Container

```bash
docker rm cont5
```

---

# Advantages

- Automated Build
- Automated Deployment
- Faster CI/CD
- Easy to Maintain
- Pipeline as Code

---

# Interview Questions

### What is a Jenkins Pipeline?

A Jenkins Pipeline is a CI/CD workflow written as code using a Jenkinsfile.

### What is a Jenkinsfile?

A Jenkinsfile is a text file that contains the pipeline definition.

### What does `agent any` mean?

It allows the pipeline to run on any available Jenkins agent.

### Which command pulls code from GitHub?

```groovy
git branch: 'main', url: 'https://github.com/...'
```

### Which command builds a Maven project?

```bash
mvn clean package
```

### Which command builds a Docker image?

```bash
docker build -t my-pipeline-05 .
```

### Which command starts a Docker container?

```bash
docker run -itd --name cont5 -p 8082:8081 my-pipeline-05
```

---

# Summary

- Jenkins Pipeline automates CI/CD.
- Pipeline consists of multiple stages.
- Stage 1 pulls code from GitHub.
- Stage 2 builds the application using Maven.
- Stage 3 builds a Docker image and runs a Docker container.
- Jenkinsfile stores the complete pipeline as code.
