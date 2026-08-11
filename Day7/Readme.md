# Jenkins Day 7 - Agent

## 📌 Topic: Jenkins Agent

### 🔹 What is Jenkins Agent?

Jenkins Agent is a machine that executes Jenkins jobs and pipelines.

- Master → Controls Jenkins
- Agent → Executes the jobs

---

## 🔹 Instance Create

Create 2 EC2 instances:

1. Master
   - Java
   - Jenkins

2. Agent
   - Java only

---

## 🔹 Change Hostname

### Master

```bash
sudo hostnamectl set-hostname master
