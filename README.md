# Migration from GitHub Actions CI/CD to Azure DevOps with ACR, AKS, and GitOps (ArgoCD)

## Overview

This project demonstrates the migration of a CI/CD pipeline from GitHub Actions to Azure DevOps for a 3-microservice application. It uses Azure Container Registry (ACR) for Docker image storage, Azure Kubernetes Service (AKS) for orchestration, and GitOps (ArgoCD) for continuous deployment.

# Application Architecture Diagram


![architecture excalidraw](https://github.com/user-attachments/assets/1f0a40fb-bc7b-4868-b73e-621dcdf312f9)

# Cloud Architecture Diagram



![azure-devops-diagram](https://github.com/user-attachments/assets/66170e1c-06cc-49f8-b849-7746953a563b)

## Prerequisites
- Azure account with access to Azure DevOps, ACR, and AKS.
- Kubernetes CLI (`kubectl`) configured for AKS.
- GitOps tool (ArgoCD) installed in the AKS cluster.
- Azure CLI for managing Azure resources.

## Migration Steps
- Setting up Azure DevOps.
- Migrating CI/CD pipelines.
- Configuring ACR and AKS.
- Implementing GitOps (ArgoCD).
- Deploying microservices.

## CI/CD Pipeline Details

- **Build Stage**: Builds Docker images for the 3 microservices (in 3 diffrent pipelines)
- **Push Stage**: Pushes the Docker images to Azure Container Registry (ACR).
- **Deploy Stage**: Deploys the microservices to AKS using Kubernetes manifests with shell script.

## GitOps Workflow
- ArgoCD continuously syncs Kubernetes manifests from azure repos to the AKS cluster with a shell script automation (it checks the latest changes within every 10s).
- Any changes to the manifests in the azure repos are automatically applied to the cluster.

## Benefits of Migration
- **Improved Integration**: Azure DevOps provides better integration with Azure services like ACR and AKS.
- **Scalability**: AKS offers better scalability and management for Kubernetes workloads.
- **GitOps Workflow**: ArgoCD enables continuous deployment and better version control for Kubernetes manifests.

## Troubleshooting
- **Issue**: Pipeline fails to push images to ACR.
  - **Solution**: Ensure the ACR service connection in Azure DevOps is correctly configured.
- **Issue**: ArgoCD fails to sync manifests.
  - **Solution**: Verify the azure repo URL and credentials in the ArgoCD configuration.

- **Issue**: Kubernetes pods fail to start and show an `ImagePullBackOff` error.
- **Solution**:
  - **Step 1**: Verify that the Docker image name and tag in the Kubernetes manifest are correct.
  - **Step 2**: Ensure the AKS cluster has access to pull images from ACR.
    - **Don't forget to create a Kubernetes Secret** to authenticate with ACR:
      ```bash
      kubectl create secret docker-registry acr-auth \
        --docker-server=<ACR_NAME>.azurecr.io \
        --docker-username=<SERVICE_PRINCIPAL_ID> \
        --docker-password=<SERVICE_PRINCIPAL_PASSWORD> \
        --docker-email=<YOUR_EMAIL>
      ```
    - Update the pod or deployment manifest to use the secret:
      ```yaml
      imagePullSecrets:
        - name: acr-auth
      ```
