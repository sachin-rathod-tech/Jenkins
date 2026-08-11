# Jenkins Day 7 - Master Agent Architecture

## Objective
Configure Jenkins Master-Agent node architecture, set up SSH authentication, and deploy applications using declarative pipelines.

---

## Prerequisites & Setup
- Delete previous cluster if exists: `kubectl delete cluster --name eks-sachin`
- Launch 2 EC2 instances (`c7i-flex.large`, 30GB SSD each)
- **Master Setup:** Install Java & Jenkins
- **Agent Setup:** Install Java only

---

## Hostname Configuration
```bash
# On Master Node
hostnamectl set-hostname master

# On Agent Node
hostnamectl set-hostname agent

## 🔹 Change Hostname

### Master

```bash
sudo hostnamectl set-hostname master
