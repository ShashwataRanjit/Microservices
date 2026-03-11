# E-Commerce Microservice Application on AWS EKS

<p align="center">
Cloud-native e-commerce platform deployed on Kubernetes using AWS infrastructure
</p>

<p align="center">
<img src="https://img.shields.io/badge/Cloud-AWS-orange">
<img src="https://img.shields.io/badge/Container-Docker-blue">
<img src="https://img.shields.io/badge/Orchestration-Kubernetes-blue">
<img src="https://img.shields.io/badge/IaC-Terraform-purple">
<img src="https://img.shields.io/badge/Communication-gRPC-green">
</p>

---

# Project Overview

This project demonstrates how a modern **cloud-native e-commerce application** can be deployed using containerized microservices on Kubernetes.

The application allows users to:

* Browse products
* Add items to a shopping cart
* Complete checkout

Each service runs inside a container and communicates with other services using **gRPC**.

The infrastructure is deployed on **Amazon Web Services using
Amazon Elastic Kubernetes Service and
Amazon Elastic Container Registry.

Infrastructure provisioning is handled using **Terraform**.

---

# Architecture

The application follows a **microservices architecture** where different services handle specific parts of the e-commerce workflow.

Key components include:

* Frontend service
* Product catalog service
* Cart service
* Checkout service
* Payment service
* Recommendation service
* Redis for cart storage

Each service runs in its own container and is managed by **Kubernetes**.

### High Level Architecture

<p align="center">
<img src="docs/architecture.png" width="900">
</p>

All services run as containers and communicate using **gRPC**.

---

# Infrastructure Flow

The deployment workflow for the application is shown below.

```
Developer
   │
   ▼
Push Code to GitHub
   │
   ▼
Run docker_image_buid_push.sh
   │
   ▼
Docker Images Built
   │
   ▼
Push Images to Amazon ECR
   │
   ▼
Terraform Creates Amazon EKS Cluster
   │
   ▼
Kubernetes Deployments Applied
   │
   ▼
Application Running on EKS
```

---

# Technologies Used

| Technology                        | Purpose                        |
| --------------------------------- | ------------------------------ |
| Docker                            | Containerization of services   |
| Kubernetes                        | Container orchestration        |
| Terraform                         | Infrastructure provisioning    |
| gRPC                              | Communication between services |
| Redis                             | Storage for shopping cart data |
| Amazon Elastic Container Registry | Container image registry       |
| Amazon Elastic Kubernetes Service | Managed Kubernetes cluster     |

---

# How to Run the Project

## 1. Clone the Repository

```bash
git clone https://github.com/Manojg-0/E-commerce-Microservice-application.git
cd E-commerce-Microservice-application
```

---

# 2. Create the Kubernetes Cluster

Navigate to the Terraform directory and create the infrastructure.

```bash
cd EKS-cluster-terraform

terraform init
terraform plan
terraform apply
```

This will provision an **Amazon EKS cluster**.

---

# 3. Connect to the Cluster

Configure kubectl to access the cluster.

```bash
aws eks --region ap-northeast-1 update-kubeconfig --name demo-cluster
```

---

# 4. Build and Push Docker Images

Navigate to the microservices directory.

```bash
cd microservices
```

Run the build script.

```bash
./docker_image_buid_push.sh
```

This script will:

* Build Docker images for all services
* Push images to **Amazon Elastic Container Registry**

---

# 5. Deploy the Application

Deploy the Kubernetes manifests.

```bash
kubectl apply -f release/kubernetes-manifests.yaml
```

---

# 6. Verify the Deployment

Check running pods.

```bash
kubectl get pods
```

Check services.

```bash
kubectl get svc
```

---

# 7. Access the Application

Get the external IP of the frontend service.

```bash
kubectl get svc frontend-external
```

Open the **EXTERNAL-IP** in your browser.

---

# Repository Structure

```
E-commerce-Microservice-application
│
├── docs
│   └── architecture.png
│
├── micro-service-demo
│
├── EKS-cluster-terraform
│
└── README.md
```

---

# Summary

This project demonstrates practical experience with:

* Cloud-native application deployment
* Containerization using Docker
* Kubernetes orchestration
* Infrastructure as Code using Terraform
* AWS services such as EKS and ECR