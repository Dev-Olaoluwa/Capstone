
# Socks Shop Microservices Deployment on Kubernetes with IaC

<img src="Images/SocksShop_diagram.png" alt="Socks Shop Architecture">

**PROJECT LIVE LINK:** [Capstone Project](http://capstone.ogdmerlin.xyz)

---

## Project Overview

The Socks Shop application is a widely-used reference application for showcasing modern cloud-native technologies. It operates as a microservices-based e-commerce platform, comprising multiple services such as product catalog, shopping cart, and user authentication. Designed for scalability, resilience, and fault tolerance, it serves as an excellent candidate for Kubernetes deployment.

This project involves deploying the Socks Shop application on a Kubernetes cluster using Infrastructure as Code (IaC). The process includes:

- Provisioning infrastructure resources on AWS
- Setting up a deployment pipeline
- Monitoring application performance and health
- Securing the infrastructure

We will utilize Terraform for infrastructure provisioning, GitHub Actions for CI/CD, Kubernetes for container orchestration, Helm for package management, Prometheus for monitoring, ELK Stack for logging, and Ansible for security.

---

## Components of the Project

- [Infrastructure Provisioning](#infrastructure-provisioning)
- [Deployment Pipeline](#deployment-pipeline)
- [Monitoring](#monitoring)
- [Logging](#logging)
- [Security](#security)
- [Conclusion](#conclusion)
- [References](#references)

---

## Project Requirements

- Terraform
- AWS Account
- Kubernetes
- Helm
- Prometheus
- ELK Stack
- Encryption
- Socks Shop Application

---

## Project Deliverables

- Terraform configuration files for AWS infrastructure provisioning
- Deployment pipeline configuration with GitHub Actions
- Kubernetes manifests for deploying the Socks Shop application
- Prometheus configuration for monitoring
- ELK Stack configuration for logging
- Ansible playbooks for security
- Documentation for running the project

---

## Getting Started

1. **Clone the Repository**

   ```sh
   git clone https://github.com/ogdmerlin/Socks-Shop
   cd Socks-Shop/terraform
   ```

2. **Set Up Infrastructure**

   - Ensure Terraform and AWS CLI are installed.
   - Initialize Terraform and apply configurations:

     ```sh
     terraform init
     terraform plan
     terraform apply --auto-approve
     ```

   - Configure `kubectl` for EKS:

     ```sh
     aws eks update-kubeconfig --name=socksShop-eks-erhzL --region=us-east-1
     ```

3. **Deploy the Application**

   - Apply Kubernetes manifests:

     ```sh
     kubectl apply -f k8s/deployment.yaml
     ```

   - Verify deployment:

     ```sh
     kubectl get all -A
     ```

   - Port-forward service to local machine:

     ```sh
     kubectl port-forward service/front-end -n sock-shop 30001:80
     ```

4. **Set Up CI/CD**

   - Ensure the workflow file is located in the `.github/workflows/` directory for GitHub Actions.

5. **Configure Monitoring**

   - Create monitoring namespace:

     ```sh
     kubectl create -f monitoring/00-monitoring-ns.yaml
     ```

   - Deploy Prometheus and Grafana:

     ```sh
     kubectl apply -f monitoring/prometheus/*.yaml
     kubectl port-forward service/prometheus 31090:9090 -n monitoring

     kubectl apply -f monitoring/grafana/*.yaml
     kubectl port-forward service/grafana 31300:3000 -n monitoring
     ```

6. **Set Up Logging**

   - Deploy ELK stack:

     ```sh
     kubectl apply -f logging/*.yaml
     kubectl port-forward service/kibana 5601:5601 -n kube-system
     ```

7. **Configure Security**

   - Obtain and apply Let's Encrypt SSL/TLS certificates to secure the application.

---

## Conclusion

This project provides hands-on experience with IaC, Kubernetes, and DevOps practices, demonstrating the value of automation and monitoring in managing microservices-based applications. You will have a fully functional deployment pipeline, including infrastructure provisioning, monitoring, logging, and security by the end of the project.

---
