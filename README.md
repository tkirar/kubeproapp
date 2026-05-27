# Kubernetes based 3‑tier application Deployment with Ingress & DNS

Architecture diagram of my Kubernetes‑based 3‑tier application. It shows how ingress traffic from AWS Load Balancer flows into NGINX Ingress, then routes to Tomcat, RabbitMQ, Memcache, and MySQL with persistent storage on Amazon EBS. This setup highlights scalability, high availability, and secure configuration with Kubernetes Secrets.”
<img width="953" height="639" alt="image" src="https://github.com/user-attachments/assets/f5072506-4fd3-43a9-b436-57574309ab93" />


## 🚀 Overview
This repository contains Kubernetes manifests and configuration files to deploy the **vProfile application stack** on a Kubernetes cluster. The stack includes:
- **Application Pod** (`vproapp`) running on port `8080`
- **Database Service** (`vprodb`) on port `3306`
- **Cache Service** (`vprocache01`) on port `11211`
- **Message Queue Service** (`vpromq01`) on port `5672`
- **Ingress Controller** (NGINX) for external routing

The project demonstrates how to expose the application via a custom domain using **AWS Load Balancer + Route53 + GoDaddy DNS**, with cluster provisioning via **Kops**.

---

## 🛠 Prerequisites
- Kubernetes cluster (Minikube for local, Kops/EKS for AWS)
- `kubectl` configured
- NGINX Ingress Controller deployed
- Domain registered (e.g., GoDaddy)
- AWS Route53 hosted zone for DNS management
- AWS CLI and Kops installed

---

## 📂 Structure
- `kubedefs/` → Kubernetes manifests (Deployments, Services, Ingress)
- `README.md` → Documentation

---

## ⚙️ Deployment Steps

### 1. Provision Cluster with Kops
Create the cluster:
```bash
kops create cluster \
  --name=<public hosted zone name> \
  --state=s3://<bucketname> \
  --zones=us-east-1a,us-east-1b \
  --node-count=2 \
  --node-size=t3.small \
  --control-plane-size=t3.medium \
  --dns-zone=<public hosted zone name> \
  --node-volume-size=12 \
  --control-plane-volume-size=12 \
  --ssh-public-key ~/.ssh/id_ed25519.pub



### 1. kops update cluster \
  --name=<public hosted zone name> \
  --state=s3://<bucketname> \
  --yes --admin

update as per you config variables
