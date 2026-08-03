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

### CI Workflow

1. Pull
2. Build
3. Test
4. Deploy

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

# Install Java

Update packages

```bash
sudo apt update
```

Install Java 17

```bash
sudo apt install openjdk-17-jdk -y
```

Verify Java

```bash
java -version
```

---

# Install Jenkins

Add Jenkins Repository Key

```bash
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
/usr/share/keyrings/jenkins-keyring.asc > /dev/null
```

Add Jenkins Repository

```bash
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
/etc/apt/sources.list.d/jenkins.list > /dev/null
```

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
```

Enable Jenkins

```bash
sudo systemctl enable jenkins
```

Check Status

```bash
sudo systemctl status jenkins
```

---

# Allow Port 8080

```bash
sudo ufw allow 8080
```

Reload Firewall

```bash
sudo ufw reload
```

---

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

Start Jenkins

```bash
sudo systemctl start jenkins
```

Enable Jenkins

```bash
sudo systemctl enable jenkins
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
