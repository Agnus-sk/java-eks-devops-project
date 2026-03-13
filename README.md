# Scalable Microservices Deployment on AWS EKS

## Overview

This project demonstrates a complete DevOps workflow for deploying a containerized Java microservice to AWS using modern DevOps tools and practices. The application is containerized using Docker, stored in Amazon ECR, and deployed on a Kubernetes cluster running on Amazon EKS. Infrastructure provisioning is automated using Terraform.

The project showcases key DevOps capabilities including containerization, infrastructure as code, Kubernetes orchestration, and cloud-native deployment.

---

## Architecture

```
GitHub Repository
       │
       ▼
CI Pipeline (GitHub Actions)
       │
       ▼
Build Java Application (Maven)
       │
       ▼
Docker Image Build
       │
       ▼
Push Image to Amazon ECR
       │
       ▼
Kubernetes Deployment
       │
       ▼
Amazon EKS Cluster
       │
       ▼
AWS Load Balancer
       │
       ▼
Users Access Application
```

Monitoring Layer:

```
Prometheus → Collects cluster and application metrics
Grafana → Visualizes metrics through dashboards
```

---

## Technologies Used

* Java Spring Boot
* Docker
* Amazon ECR
* Kubernetes
* AWS EKS
* Terraform
* Maven
* Git & GitHub
* Prometheus
* Grafana

---

## Project Structure

```
java-eks-devops-project
│
├── app
│   └── springboot-app
│
├── docker
│   └── Dockerfile
│
├── terraform
│   ├── main.tf
│   ├── vpc.tf
│   ├── eks.tf
│   └── variables.tf
│
├── k8s
│   ├── deployment.yaml
│   ├── service.yaml
│   ├── ingress.yaml
│   └── hpa.yaml
│
├── monitoring
│   ├── prometheus.yaml
│   └── grafana.yaml
│
└── README.md
```

---

## Features

* Containerized Spring Boot application using Docker
* Docker image stored in Amazon ECR
* Infrastructure provisioning using Terraform
* Kubernetes deployment using Amazon EKS
* Load balancing for external access
* Horizontal Pod Autoscaling for dynamic scaling
* Monitoring using Prometheus and Grafana

---

## Step-by-Step Implementation

### 1. Create Spring Boot Application

A simple REST API was developed using Spring Boot.

Endpoint:

```
GET /hello
```

Response:

```
Hello from AWS EKS DevOps Project!
```

---

### 2. Dockerize the Application

Dockerfile used to containerize the application:

```
FROM eclipse-temurin:17-jdk-jammy

WORKDIR /app

COPY target/eks-demo-0.0.1-SNAPSHOT.jar app.jar

EXPOSE 8081

ENTRYPOINT ["java","-jar","app.jar"]
```

Build Docker image:

```
docker build -t eks-demo-app .
```

Run container locally:

```
docker run -p 8081:8081 eks-demo-app
```

---

### 3. Push Docker Image to Amazon ECR

Create ECR repository:

```
aws ecr create-repository --repository-name eks-demo-app --region ap-south-1
```

Authenticate Docker with ECR:

```
aws ecr get-login-password --region ap-south-1 \
| docker login --username AWS --password-stdin <account-id>.dkr.ecr.ap-south-1.amazonaws.com
```

Tag Docker image:

```
docker tag eks-demo-app:latest <account-id>.dkr.ecr.ap-south-1.amazonaws.com/eks-demo-app:latest
```

Push image to ECR:

```
docker push <account-id>.dkr.ecr.ap-south-1.amazonaws.com/eks-demo-app:latest
```

---

### 4. Provision Infrastructure with Terraform

Terraform is used to create:

* VPC
* Subnets
* Internet Gateway
* Amazon EKS cluster
* Worker node group

Commands used:

```
terraform init
terraform plan
terraform apply
```

---

### 5. Deploy Application to Kubernetes

Application deployed using Kubernetes manifests:

```
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

---

### 6. Enable Auto Scaling

Horizontal Pod Autoscaler configured to scale pods based on CPU usage.

---

### 7. Monitoring

Prometheus collects cluster metrics and Grafana visualizes them using dashboards.

---

## Learning Outcomes

Through this project the following DevOps skills were demonstrated:

* Infrastructure as Code using Terraform
* Containerization using Docker
* Kubernetes orchestration
* Cloud-native deployment using AWS EKS
* CI/CD integration
* Monitoring and observability

---

## Author

Agnussk
DevOps Enthusiast | Full Stack Developer
Skills: Docker, Kubernetes, Terraform, AWS, Python, Django
