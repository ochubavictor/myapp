# Full Stack Deployment: Docker, HTTPS & CI/CD

## Overview
A company has an application that needs to be deployed in a structured and reliable way. 
It must be accessible through a custom domain, secured with HTTPS, and updated automatically 
whenever new code is pushed.

This project solves that problem end to end.

## Architecture
GitHub → GitHub Actions → Azure VM → Docker Container → Nginx → HTTPS Domain

## Tech Stack
- Cloud: Microsoft Azure (VM)
- Containerization: Docker
- Web Server: Nginx (reverse proxy)
- SSL/HTTPS: Let's Encrypt via Certbot
- CI/CD: GitHub Actions
- OS: Ubuntu 22.04 LTS

## What This Setup Delivers
- Consistent application deployment every time
- Secure public access over HTTPS
- Automatic updates on every code push to main
- Zero manual steps after initial setup
- A clean and reliable delivery workflow

## Project Structure
myapp/
├── app/
│   ├── index.js
│   └── package.json
├── Dockerfile
└── .github/
└── workflows/
└── deploy.yml
## Setup & Deployment

### 1. Azure VM
- Created Ubuntu 22.04 LTS VM on Azure
- Opened inbound ports: 22 (SSH), 80 (HTTP), 443 (HTTPS)

### 2. Docker
- Installed Docker on the VM
- Built and ran the app as a container on port 3000

### 3. Nginx
- Installed Nginx as a reverse proxy
- Routed traffic from port 80 to the app on port 3000

### 4. Custom Domain & HTTPS
- Pointed custom domain A records to the VM public IP
- Secured with SSL certificate using Certbot and Let's Encrypt

### 5. GitHub Actions (CI/CD)
- Configured GitHub Actions to automatically deploy on every push to main
- Pipeline SSHs into the VM, pulls latest code, rebuilds Docker image and restarts container

## Screenshots

### App Live with HTTPS
![HTTPS](images/https-screenshot.png)

### GitHub Actions Pipeline
![CI/CD](images/github-actions.png)

### Docker Container Running
![Docker](images/docker-ps.png)

## Key Lessons
- DNS propagation takes time — certbot will fail if you run it too early
- Docker permissions on Linux require adding user to the docker group
- Nginx must be configured correctly before certbot can issue a certificate
- The order of setup matters: app → Docker → Nginx → DNS → HTTPS → CI/CD

## Live Demo
🌐 [tradeinsurex.online](https://tradeinsurex.online)

## Repository
[github.com/ochubavictor/myapp](https://github.com/ochubavictor/myapp)