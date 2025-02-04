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
