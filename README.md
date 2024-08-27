
# 2048 Game Deployment on AWS EKS with Fargate

Welcome to my project repository! Here, I’ve documented my journey of deploying the popular 2048 game on a Kubernetes cluster using AWS Elastic Kubernetes Service (EKS) and AWS Fargate. This project is a great example of leveraging Kubernetes for container orchestration and AWS Fargate for seamless, serverless infrastructure management.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Architecture Overview](#architecture-overview)
- [Setup Instructions](#setup-instructions)
  - [1. Installing EKS](#1-installing-eks)
  - [2. Configuring IAM and ALB Controller](#2-configuring-iam-and-alb-controller)
  - [3. Deploying the 2048 Game](#3-deploying-the-2048-game)
- [Ingress Configuration](#ingress-configuration)
- [Fargate Profiles and Cluster Management](#fargate-profiles-and-cluster-management)
- [Troubleshooting and Tips](#troubleshooting-and-tips)
- [Images and Visual Walkthrough](#images-and-visual-walkthrough)
- [Contributing](#contributing)
- [License](#license)

## Prerequisites

Before you begin, make sure you have the following:

- AWS CLI installed and configured with the appropriate credentials.
- `eksctl` installed to help manage EKS clusters.
- `kubectl` installed for interacting with the Kubernetes cluster.
- An AWS account with the necessary permissions to create EKS clusters and manage resources.

I’ve detailed the setup in the [prerequisites.md](prerequisites.md) file to help you get started quickly.

## Architecture Overview

In this project, I used AWS EKS to manage a Kubernetes cluster and configured AWS Fargate profiles to run the game pods in a serverless environment. This setup uses an AWS Application Load Balancer (ALB) to route external traffic to the Kubernetes cluster, ensuring high availability and scalability.

## Setup Instructions

### 1. Installing EKS

I began by setting up an EKS cluster in the `eu-west-3` region. By following the steps in [installing-eks.md](installing-eks.md), you can replicate the process to configure your network and security settings.

### 2. Configuring IAM and ALB Controller

After setting up the cluster, I configured the necessary IAM roles and policies for the AWS Load Balancer Controller. This was crucial to ensure the Kubernetes Ingress resources could interact with AWS resources effectively. I’ve documented each step in [alb-controller-add-on.md](alb-controller-add-on.md) and [configure-oidc-connector.md](configure-oidc-connector.md).

### 3. Deploying the 2048 Game

Once everything was set up, I deployed the 2048 game using Kubernetes manifests. You can find these files in [sample-app.md](sample-app.md). To deploy the game, run:

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl apply -f ingress.yaml
```

## Ingress Configuration

For this project, I configured an Ingress resource to use an AWS ALB to manage incoming traffic. The AWS Load Balancer Controller automatically provisioned and managed the ALB, allowing for seamless routing and scaling of the application. You can find more details in [2048-app-deploy-ingress.md](2048-app-deploy-ingress.md).

## Fargate Profiles and Cluster Management

To run the game pods in a serverless environment, I set up AWS Fargate profiles. This setup allowed me to avoid managing EC2 instances and focus on optimizing the application’s performance. You can follow my process in [installing-eks.md](installing-eks.md).

## Troubleshooting and Tips

During the project, I encountered a few challenges:
- Ensuring all IAM roles and policies were correctly configured to grant the necessary permissions was critical.
- I used `eksctl` and `kubectl` to monitor the status of the EKS cluster and Fargate profiles, which helped in quickly resolving any issues.
- AWS CloudFormation was also a great tool for managing and monitoring the underlying AWS resources.

## Images and Visual Walkthrough

Here are some images that capture the steps I took to set up the 2048 game on AWS EKS with Fargate:

- **EKS Cluster Creation**: ![EKS Cluster Creation](EKCTL%20CREATE.jpg)
- **Fargate Profiles**: ![Fargate Profiles](FARGATE.jpg)
- **IAM and ALB Setup**: ![IAM and ALB Setup](ALB%20IAM%20POLICY.jpg)
- **Ingress and Load Balancer Configuration**: ![Ingress Configuration](INGRESS%20CREATED%20LOADBALANCER.jpg)
- **Application Deployment**: ![Application Deployment](KUBECTL%20APPLY%20-F.jpg)

You can view these images in the repository for a step-by-step visual guide.
