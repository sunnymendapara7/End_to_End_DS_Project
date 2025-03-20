
# End-to-End Data Science Project

This repository contains a complete end-to-end Machine Learning pipeline, from data ingestion to model deployment using AWS and GitHub Actions.

## Workflows - ML Pipeline

1. **Data Ingestion**
2. **Data Validation**
3. **Data Transformation** - Feature Engineering, Data Preprocessing
4. **Model Training**
5. **Model Evaluation** - Using MLflow and DagsHub

## Steps to Use This Repository

1. Update `config.yaml`
2. Update `schema.yaml`
3. Update `params.yaml`
4. Update the entity
5. Update the configuration manager in `src/config`
6. Update the components
7. Update the pipeline
8. Update `main.py`

---

# AWS CI/CD Deployment with GitHub Actions

## Prerequisites

1. **AWS Account** - Ensure you have access to AWS services.
2. **GitHub Repository** - Fork or clone this repository.
3. **Docker Installed** - Required for building container images.

---

## Deployment Steps

### 1. Login to AWS Console

### 2. Create IAM User for Deployment

Create an IAM user with specific access policies:

#### Required AWS Permissions:

- **EC2 Access** - To manage virtual machines.
- **ECR Access** - Elastic Container Registry for storing Docker images.

#### IAM Policies to Attach:

- `AmazonEC2ContainerRegistryFullAccess`
- `AmazonEC2FullAccess`

---

### 3. Create an ECR Repository

- Navigate to AWS ECR and create a repository to store Docker images.
- Save the repository URI (Example: `amazonaws.com/simple-app`).

---

### 4. Create an EC2 Instance (Ubuntu)

- Launch an EC2 instance and ensure it has a security group allowing SSH and necessary ports.

---

### 5. Install Docker on EC2

Run the following commands on your EC2 instance:

```sh
sudo apt-get update -y
sudo apt-get upgrade -y
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker ubuntu
newgrp docker
```

---

### 6. Configure EC2 as a Self-Hosted GitHub Runner

- Navigate to GitHub Repository → Settings → Actions → Runners
- Click **New self-hosted runner**, choose the OS, and follow the setup instructions.

---

### 7. Setup GitHub Secrets

Go to GitHub Repository → Settings → Secrets → Actions and add the following:

| Secret Name               | Value Example                 |
| ------------------------- | ----------------------------- |
| `AWS_ACCESS_KEY_ID`     | `<your-access-key>`         |
| `AWS_SECRET_ACCESS_KEY` | `<your-secret-key>`         |
| `AWS_REGION`            | `us-east-1`                 |
| `AWS_ECR_LOGIN_URI`     | `.ap-south-1.amazonaws.com` |
| `ECR_REPOSITORY_NAME`   | `simple-app`                |

---

### 8. Deployment Workflow Overview

1. **Build the Docker image of the source code**
2. **Push the Docker image to AWS ECR**
3. **Launch an EC2 instance**
4. **Pull the Docker image from ECR to EC2**
5. **Run the containerized application on EC2**

Now project is fully set up for an end-to-end ML pipeline with AWS CI/CD! 🚀
