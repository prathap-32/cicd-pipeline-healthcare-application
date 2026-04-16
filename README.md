# End-to-End CI/CD Pipeline using Jenkins, Docker, and Kubernetes

This project demonstrates a complete **CI/CD pipeline implementation** to automate the build, delivery, and deployment of a containerized application using:

- **Jenkins** (CI/CD Automation)  
- **Docker** (Containerization)  
- **Kubernetes (Minikube)** (Orchestration & Deployment)  

---

## Overview

The pipeline enables seamless transition from **code commit to production deployment**, ensuring:

- Faster delivery  
- Reduced manual effort  
- Scalable application deployment  
- Zero-downtime updates using rolling strategy  

---

## CI/CD Workflow

```
Developer Commit → GitHub Repository → Jenkins Trigger
        ↓
Source Code Checkout
        ↓
Docker Image Build
        ↓
Docker Image Push (Docker Hub)
        ↓
Kubernetes Apply (YAML Files)
        ↓
Update Deployment Image
        ↓
Rolling Update
        ↓
Application Running in Kubernetes

```

---

## Pipeline Stages

### 1. Source Code Management
- Code stored in GitHub repository  
- Includes:
  - Application code  
  - Dockerfile  
  - Kubernetes manifests  
  - Jenkinsfile  

---

### 2. Jenkins Trigger
Pipeline starts automatically when:
- Code is pushed to GitHub (Webhook / Poll SCM)

---

### 3. Code Checkout

```bash
git clone <repository-url>
```

---

### 4. Docker Build Stage

```bash
docker build -t <dockerhub-username>/web-app:<build-number> .
docker tag <dockerhub-username>/web-app:<build-number> <dockerhub-username>/web-app:latest
```

---

### 5. Docker Push Stage

```bash
docker push <dockerhub-username>/web-app:<build-number>
docker push <dockerhub-username>/web-app:latest
```

---

### 6. Kubernetes Deployment

```bash
kubectl apply -f k8s/web-app-configmap.yaml
kubectl apply -f k8s/web-app-service.yaml
kubectl apply -f k8s/web-app-deployment.yaml
```

---

### 7. Update Deployment Image

```bash
kubectl set image deployment/web-app web-app=<dockerhub-username>/web-app:<build-number>
```

---

### 8. Rolling Update Strategy

- New pods are created gradually  
- Old pods are terminated step by step  
- Zero downtime during deployment  

---

### 9. Verification Stage

```bash
kubectl rollout status deployment/web-app
kubectl get pods
kubectl get svc
```

---

## Kubernetes Architecture

- **Deployment** → Manages application pods  
- **Service** → Exposes application  
- **ConfigMap** → Stores configuration  
- **Secret** → Stores sensitive data  

---

## Tools Used

| Tool | Purpose |
|------|--------|
| Jenkins | CI/CD automation |
| Docker | Containerization |
| Docker Hub | Image registry |
| Kubernetes | Container orchestration |
| GitHub | Version control |
| Minikube | Local Kubernetes cluster |

---

## Scalability Benefits

- Automated build and deployment  
- Faster release cycles  
- Reduced human errors  
- Supports rolling updates  
- Easily scalable across environments  

---

## Key Outcome

This pipeline enables:

> 🔹 Automated deployment from GitHub to Kubernetes  
> 🔹 Continuous integration and continuous delivery  
> 🔹 Scalable and reliable application deployment  

---

## Future Enhancements

- Add Persistent Volume (PVC) for database  
- Implement Ingress Controller  
- Add Monitoring (Prometheus + Grafana)  
- Add Logging (ELK Stack)  
- Use Helm Charts for deployment  

---

## Author

**Prathap G**  
DevOps & Cloud Enthusiast
