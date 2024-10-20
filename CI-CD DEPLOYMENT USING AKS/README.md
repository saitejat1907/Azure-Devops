# Voting Application

This repository contains a 3-tier voting application with the following components:

1. **Front-end Web App (Python):** Allows users to vote between two options.
2. **Redis:** Collects new votes.
3. **.NET Worker:** Consumes votes from Redis and stores them in a Postgres database.
4. **Postgres Database:** Stores votes, backed by a Docker volume.
5. **Node.js Web App:** Displays real-time voting results.

## Architecture

- **Front-end:** Python web app (Flask) for voting.
- **Redis:** Acts as the queue for storing incoming votes.
- **Worker:** .NET Core application that processes votes from Redis and stores them in the Postgres database.
- **Postgres:** Persistent storage for votes.
- **Results:** Node.js app for real-time results display.

## Setup

### Pre-requisites

- Azure Kubernetes Service (AKS) cluster
- Azure DevOps project
- ArgoCD for GitOps-based deployments
- Azure Container Registry (ACR)
- Azure Virtual Machine (for agent)
- Docker
- Helm
- Kubernetes CLI (kubectl)
- Redis, Postgres, and .NET runtime

### Deployment Overview

- **CI Pipeline:** 
  - Created in Azure DevOps.
  - Builds Docker images for all tiers.
  - Stores the images in Azure Container Registry (ACR).
  - Uses an Azure VM as the build agent.

- **CD Pipeline:** 
  - The front-end web app is deployed into the AKS Kubernetes cluster using ArgoCD (GitOps).

### Steps to Deploy

1. Clone the repository from GitHub.

   ```bash
   git clone https://github.com/saitejat1907/example-voting-app
   cd voting-app
   ```

2. Build Docker images for the various components using the CI pipeline in Azure DevOps.

   - The pipeline is configured to:
     - Build Docker images for the Front-end, Worker, and Results tiers.
     - Push the Docker images to Azure Container Registry (ACR).
     - Use an Azure VM as the agent.

3. Deploy to AKS using ArgoCD.

   - Ensure ArgoCD is configured for your AKS cluster.
   - Link the repository for GitOps deployment.

   ```bash
   kubectl create namespace argocd
   kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

   ```

4. Check the deployment status by verifying the running pods and services in AKS.

   Access the front-end voting app via the AKS service IP.
   ```bash
   kubectl get pods
   kubectl get services
   ```

## CI/CD Pipelines

- **CI Pipeline:**
  - The CI pipeline builds Docker images for all three tiers (Front-end, Redis, Worker, and Node.js Results).
  - The images are stored in Azure Container Registry (ACR).
  - The build agent is an Azure Virtual Machine.

- **CD Pipeline:**
  - The CD pipeline deploys the front-end to AKS using ArgoCD.

## Technologies Used

- Python (Flask)
- Redis
- .NET Core Worker
- Postgres
- Node.js
- Docker
- Kubernetes (AKS)
- Azure Container Registry (ACR)
- ArgoCD
- Azure DevOps
- Azure Virtual Machine (as build agent)

## Contributing

Feel free to submit issues or pull requests if you would like to contribute to the project!
