# Node.js Application - ArgoCD Deployment

This directory contains the Kubernetes manifests and ArgoCD configuration for deploying a Node.js application using GitOps.

## Structure

```
my-k8s-app/
├── app.yaml              # ArgoCD Application definition
├── project.yaml          # ArgoCD Project definition
├── kustomization.yaml    # Kustomize configuration
├── deployment.yaml       # Kubernetes Deployment
├── service.yaml          # Kubernetes Services
├── ingress.yaml          # Kubernetes Ingress
├── configmaps/
│   └── app-cm.yaml       # Application ConfigMap
└── README.md             # This file
```

## ArgoCD Setup

### 1. Create ArgoCD Project

```bash
kubectl apply -f project.yaml
```

### 2. Create ArgoCD Application

```bash
kubectl apply -f app.yaml
```

### 3. Access ArgoCD UI

- URL: https://localhost:8080/applications
- Username: admin
- Password: Get with `kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d`

## Application Features

- **Automated Sync**: Application automatically syncs when Git repository changes
- **Self-Healing**: ArgoCD automatically corrects drift
- **Prune**: Removes resources not in Git
- **Health Checks**: Built-in health monitoring

## Git Repository

The application expects the following Git repository structure:

```
k8s-nodejs-app/
└── my-k8s-app/
    ├── app.yaml
    ├── project.yaml
    ├── kustomization.yaml
    ├── deployment.yaml
    ├── service.yaml
    ├── ingress.yaml
    └── configmaps/
        └── app-cm.yaml
```

## Deployment Status

Check application status:

```bash
kubectl get applications -n argocd
kubectl describe application nodejs-app -n argocd
```
