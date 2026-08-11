# Jenkins Day 7 - Master Agent Architecture

## Objective
Configure Jenkins Master-Agent node architecture, set up SSH authentication, and deploy applications using declarative pipelines.

---

## Prerequisites & Setup
- Launch 2 EC2 instances (`c7i-flex.large`, 30GB SSD each)
- **Master Setup:** Install Java & Jenkins
- **Agent Setup:** Install Java only

---

## 🔹 Change Hostname

### On Master Node
```
hostnamectl set-hostname master
```
### On Agent Node
```
hostnamectl set-hostname agent
```

## Master

### SSH Authentication Workflow

Master Node
   |
[ssh-keygen] -> Generates Public/Private Key
   |
[Copy Public Key] -> Paste into Agent's authorized_keys
   |
Agent Node

---

# Master Node
   |
[ssh-keygen] -> Generates Public/Private Key
   |
[Copy Public Key] -> Paste into Agent's authorized_keys
   |
Agent Node

# Step 2: Agent SSH Authorization

## Navigate to SSH directory on Agent
cd .ssh/

## Paste Master's public key
vim authorized_keys

## Optional: Set permissions
chmod 777 authorized_keys

# step 3: Jenkins UI Configuration
### Add Credentials
* Go to Manage Jenkins -> Credentials
* Select SSH username with private key
* ID: agent-cred
* Username: ubuntu
* Private Key: Select Enter directly and paste Master's Private Key

### Add Node

#### Go to Manage Jenkins -> Nodes -> New Node

* **Node Name:** agent01
* **Type:** Permanent Agent
* **Number of executors:** 1
* **Remote root directory:** /home/ubuntu/main
* **Labels:** sachin
* **Usage:** Use this node as much as possible
* **Launch Method:** Launch agents via SSH
* **Host:** Agent_Public_IP
* **Host Key Verification Strategy:** Non-verifying Verification Strategy

---

## add job

#### Pipeline 
```
pipeline {
    agent {
        label 'sachin'
    }
    stages {
        stage('deploy') {
            steps {
                sh 'docker pull rathods6/netflix:v5'
                sh 'docker run -itd --name agent -p 8085:80 rathods6/netflix:v5'
            }
        }
    }
}
```

