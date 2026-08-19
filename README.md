# Namegen DevOps Deployment on AWS EKS

This repository contains the source code, Docker configuration, Kubernetes manifests, and CI/CD automation for deploying the namegen web application on AWS Elastic Kubernetes Service (EKS) with persistent MongoDB storage.

---

## Architecture Overview

The application is deployed on an AWS EKS cluster with managed node groups. External HTTP traffic routes through an AWS Elastic Load Balancer to the Node.js frontend pods, which communicate internally with a MongoDB StatefulSet backed by AWS EBS persistent storage (gp3).

![Architecture Diagram](architecture-diagram.jpg)

---

## Application URL & Endpoint

* **LoadBalancer External DNS:** \k8s-default-namegens-5f08c13c48-6e6692ab5bb93a51.elb.us-east-1.amazonaws.com\
* **Port:** \80:30293/TCP\

---

## Repository Structure

\\\
.
|-- server.js                   # Application entry point
|-- package.json                # Node.js dependencies
|-- Dockerfile                  # Container build instructions
|-- architecture-diagram.jpg    # Architecture & CI/CD Diagram
|-- eksctl/
|   \-- cluster.yaml            # EKS Cluster provision configuration
|-- k8s/
|   |-- app-deployment.yaml     # App Deployment
|   |-- app-service.yaml        # LoadBalancer Service
|   \-- mongodb-statefulset.yaml# MongoDB StatefulSet & Service
\-- screenshots/
    |-- app-cleared-db.png
    |-- app-saved-names.png
    \-- kubectl-cluster-status.png
\\\

---

## CI/CD Pipeline & Deployment Instructions

### 1. Provision AWS EKS Cluster
\\\ash
eksctl create cluster -f eksctl/cluster.yaml
\\\

### 2. Deploy Kubernetes Resources
\\\ash
kubectl apply -f k8s/
\\\

### 3. Verify Deployment
\\\ash
kubectl get pods,svc,deployments,statefulsets
\\\

---

## Screenshots

### Active Kubernetes Cluster Resources & LoadBalancer Address
![Kubectl Status](screenshots/kubectl-cluster-status.png)

### Running Application & MongoDB Persistence
![App Saved Names](screenshots/app-saved-names.png)
