# Jenkins Day 1 - Introduction & Installation

## Objective

Learn the basics of Jenkins and install Jenkins on an Ubuntu server.

---

# What is Jenkins?

**Jenkins is an open-source automation server**.

It is used to automate:

- Building
- Testing
- Deploying software

Jenkins is written in Java.

It can:

- Build applications
- Run multiple tests
- Create Docker images
- Deploy applications
- Automate repetitive tasks

> **Definition:** Jenkins is a CI/CD tool that automates Build, Test, and Deployment.

---


# What is CI/CD?

### Continuous Integration (CI)

Developers frequently push code to GitHub. Jenkins automatically builds and tests the application.

### Continuous Delivery (CD)

Jenkins automatically prepares the application for deployment.

### Continuous Deployment

Jenkins automatically deploys the application after successful testing.

---

# Jenkins Architecture

```
Developer
     │
     ▼
GitHub Repository
     │
     ▼
Jenkins Controller
     │
     ▼
Jenkins Agent
     │
     ▼
Build → Test → Deploy
```

---

### CICD Workflow
```
1. Pull
2. Build
3. Test
4. Deploy
```
---

# Jenkins Features

- Open Source
- Free to Use
- 2000+ Plugins
- Easy GitHub Integration
- Supports Docker
- Supports Kubernetes
- Pipeline as Code
- Distributed Builds

---

# Prerequisites

- Ubuntu 22.04
- Java 17
- Internet Connection
- Sudo User

---

# Install Jenkins

### flow official documentation
```
jenkins install for ubuntu
```
<img width="844" height="209" alt="image" src="https://github.com/user-attachments/assets/db2a270b-9075-4409-bc08-47a08dc45f81" />

<img width="899" height="319" alt="image" src="https://github.com/user-attachments/assets/7670477d-1a96-433a-8864-192f79130bda" />


### Install Java 17

```bash
sudo apt update
sudo apt install fontconfig openjdk-21-jre
java -version
```

## Long Term Support release
<img width="988" height="403" alt="image" src="https://github.com/user-attachments/assets/dc59568a-f741-4f40-831c-0c790efe2b27" />

```
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2026.key
echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt update
sudo apt install jenkins
```
---


Update Repository

```bash
sudo apt update
```

Install Jenkins

```bash
sudo apt install jenkins -y
```

---

# Start Jenkins

```bash
sudo systemctl start jenkins
sudo systemctl enable jenkins
sudo systemctl status jenkins
```

---

# Allow Port 8080 in your security group


# Access Jenkins

```
http://<EC2-Public-IP>:8080
```

Example

```
http://13.234.xx.xx:8080
```

---

# Get Initial Admin Password

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Copy the password and paste it into the Jenkins Unlock screen.

---

# Initial Jenkins Setup

- Unlock Jenkins
- Install Suggested Plugins
- Create First Admin User
- Login to Jenkins Dashboard

---

# Useful Commands

Check Version

```bash
java -version
```

Check Jenkins Status

```bash
sudo systemctl status jenkins
```

Restart Jenkins

```bash
sudo systemctl restart jenkins
```

Stop Jenkins

```bash
sudo systemctl stop jenkins
```


---

# Default Port

```
8080
```

---

# Default Jenkins Directory

```
/var/lib/jenkins
```

---

# Interview Questions

### What is Jenkins?

Jenkins is an open-source automation server used for CI/CD.

### Which language is Jenkins written in?

Java.

### Which port does Jenkins use?

8080.

### Which Java version is recommended?

Java 17 or later.

### Where is the initial admin password stored?

```
/var/lib/jenkins/secrets/initialAdminPassword
```

### Which command starts Jenkins?

```bash
sudo systemctl start jenkins
```

---

# Summary

- Jenkins is an automation server.
- Jenkins is used for CI/CD.
- Install Java before Jenkins.
- Jenkins runs on port **8080**.
- Unlock Jenkins using the initial admin password.
- Install plugins and create the first admin user.
