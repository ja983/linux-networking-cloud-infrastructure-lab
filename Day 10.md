AWS EC2 Linux Server Deployment & Hardening Lab 🚀

This repository documents the hands-on project and lab for Module 02: Linux, Networking & Cloud Infrastructure (Day 10), focusing on provisioning, securing, and deploying a production-ready Linux server environment on AWS EC2.

🛠️ Architecture & Tech Stack

Cloud Platform: AWS EC2 (t3.micro instance running Ubuntu LTS)

Web Server: Nginx

Security & Firewalls: UFW (Uncomplicated Firewall), AWS Security Groups, and SSH key-based hardening

Tools: Bash, OpenSSH, cURL, Git

📋 Step-by-Step Deployment Guide

Phase 1: Provisioning & Initial Connection

Launch an Ubuntu LTS virtual machine instance on AWS EC2.

Establish the initial SSH connection using your private key:

ssh -i <your-key.pem> ubuntu@<your-ec2-public-ip>


Phase 2: System Updates & User Management

Update system package repositories:

sudo apt update && sudo apt upgrade -y


Create a dedicated non-root administrative user (devopsadmin) with sudo privileges:

sudo adduser devopsadmin
sudo usermod -aG sudo devopsadmin


Transfer your SSH public key to the new user account and secure permissions:

sudo mkdir -p /home/devopsadmin/.ssh
sudo cp ~/.ssh/authorized_keys /home/devopsadmin/.ssh/authorized_keys
sudo chown -R devopsadmin:devopsadmin /home/devopsadmin/.ssh
sudo chmod 700 /home/devopsadmin/.ssh
sudo chmod 600 /home/devopsadmin/.ssh/authorized_keys


Phase 3: SSH Hardening

Open the SSH daemon configuration file:

sudo nano /etc/ssh/sshd_config


Ensure the following parameters are strictly configured:

PermitRootLogin no

PasswordAuthentication no

PubkeyAuthentication yes

Test configuration syntax and restart the SSH service:

sudo sshd -t
sudo systemctl restart ssh


Phase 4: Firewall Configuration (UFW & AWS Security Groups)

Install Nginx so the UFW application profile becomes available:

sudo apt install nginx -y


Configure host-based UFW rules:

sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow OpenSSH
sudo ufw allow 'Nginx HTTP'
sudo ufw enable


Configure AWS EC2 Security Group Inbound Rules in the AWS Console:

HTTP (Port 80): TCP, 0.0.0.0/0

SSH (Port 22): TCP, Trusted IP / 0.0.0.0/0

Phase 5: Web Service Deployment & Verification

Enable and start the Nginx service:

sudo systemctl enable nginx
sudo systemctl start nginx


Deploy a custom HTML landing page:

echo "<h1>Hello from Day 10 Lab - Cloud Infrastructure Deployed Successfully!</h1>" | sudo tee /var/www/html/index.html


Validate local and remote connectivity:

curl -I http://localhost
curl -I http://<your-ec2-public-ip>


🏆 Results & Verification

Successfully verified HTTP 200 OK response headers via terminal cURL and external browser testing.

Enforced least-privilege access and locked down SSH against unauthorized brute-force attempts.
