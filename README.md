# Blue-Green Deployment Workflow for `hello-app`

This repository demonstrates the Blue-Green deployment strategy for `hello-app` using Kubernetes and GitHub Actions.

## Workflow Overview

1. **Build and Push Docker Image**:  
   The application is containerized and pushed to a container registry (https://hub.docker.com/r/dbatruh/github-actions-example).

2. **Deploy to Green Environment**:  
   The updated version is deployed to the `green` environment while the `blue` environment remains active.

3. **Test Green Environment**:  
   Smoke tests are executed to validate the new deployment.

4. **Switch Traffic to Green**:  
   Once validated, the Kubernetes service routes all traffic to the `green` environment.

5. **Clean Up**:  
   After the `green` environment is stable, the `blue` environment is be removed.

## Automating with GitHub Actions

The `.github/workflows/ci-cd-workflow.yaml` file automates this workflow:
- Builds the Docker image.
- Pushes the image to a registry.
- Deploys to Kubernetes cluster in GKE.
- Executes tests and switches traffic upon success.
- Updates Kubernetes resources and commits updated files to repository.

---

For manual deployment steps, Kubernetes manifests are located in the `k8s/` directory.
