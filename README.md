# ArgoCD GitOps Project

This project demonstrates GitOps-style Kubernetes deployments using ArgoCD.

## Features
- Git-based deployment automation
- ArgoCD auto-sync with GitHub
- Kubernetes manifests version controlled in Git

## Setup Steps

1. Build and push Docker image:
```
docker build -t yourdockerhubusername/gitops-demo:latest ./app
docker push yourdockerhubusername/gitops-demo:latest
```

2. Install ArgoCD in your Kubernetes cluster:
```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

3. Apply the ArgoCD Application manifest:
```
kubectl apply -f argocd/app.yaml
```

4. Access ArgoCD UI and login:
```
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

Then open http://localhost:8080

Default username: admin  
Password: Run `kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}" | base64 -d`

5. Your app will be deployed and synced automatically!
