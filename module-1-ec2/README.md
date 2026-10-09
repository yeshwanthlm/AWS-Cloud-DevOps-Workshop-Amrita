# Module 1 — Host a Website on AWS EC2

> This module will be explained live during the workshop. Details will be unlocked after the session.

---

## What You Will Learn

- How to launch a virtual server (EC2 instance) on AWS
- How to connect to it over SSH
- How to install a web server (Apache) on it
- How to deploy a static HTML/CSS website manually

---

## Prerequisites

Make sure you have completed everything in the [Prerequisites](../prerequisites/README.md) section before starting this module.

---

## 🔒 Step-by-step Instructions:

### Step 1: Launch an EC2 Instance
1. Log in to [AWS Console](https://console.aws.amazon.com)
2. Go to **EC2 → Launch Instance**
3. Fill in the details:
   - **Name:** `amrita-workshop-server`
   - **AMI:** Ubuntu Server 22.04 LTS (Free Tier eligible)
   - **Instance type:** `t2.micro or t3.micro` (Free Tier eligible)
   - **Key pair:** Create a new key pair → name it `amrita-key` → download the `.pem` file
   - **Security Group:** Allow the following inbound rules:
     | Type  | Port | Source    |
     |-------|------|-----------|
     | SSH   | 22   | My IP     |
     | HTTP  | 80   | 0.0.0.0/0 |
4. Click **Launch Instance**
5. Wait ~1 minute for the instance to reach **Running** state

### Step 2: Connect to EC2 via SSH
```bash
# Fix permissions on your key file (required on Mac/Linux)
chmod 400 amrita-key.pem

# Connect (replace <PUBLIC_IP> with your EC2 public IP)
ssh -i "amrita-key.pem" ubuntu@<PUBLIC_IP>
```

### Step 3: Install Apache and Deploy the Website
```bash
# Update package lists and upgrade existing packages
sudo apt update -y
sudo apt upgrade -y

# Install Apache web server
sudo apt install apache2 -y

# Start and enable Apache to run on boot
sudo systemctl start apache2
sudo systemctl enable apache2

# Clone the workshop repository
git clone https://github.com/yeshwanthlm/AWS-Cloud-DevOps-Workshop-Amrita.git

# Move into the project folder
cd AWS-Cloud-DevOps-Workshop-VVCE/module-1-ec2

# List the files to verify
ls -lrt

# Copy website files to Apache's web root
sudo mv * /var/www/html/
```

### Step 4: View the Website
- Open your browser and go to: `http://<PUBLIC_IP>`
- You should see the resume website

> 💡 **What just happened?** You manually SSHed into a server, installed a web server, and copied your files. This is the "old way" — now let's automate it.

---
---

[← Back to Main](../README.md) | [Next Module: CI/CD with GitHub Actions →](../module-2-cicd/README.md)
