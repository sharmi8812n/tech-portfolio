# Kubernetes – Overview & Basics

## What is Kubernetes?

Kubernetes (often abbreviated as K8s) is an open-source container orchestration platform that automates the deployment, scaling, and management of containerized applications. It enables organizations to run distributed systems resiliently with zero downtime and efficient resource utilization.

---

## Key Concepts

- **Cluster:** A set of machines (nodes) running Kubernetes.  
- **Node:** A worker machine (physical or virtual) in the cluster.  
- **Pod:** The smallest deployable unit, which can contain one or more containers.  
- **Deployment:** Defines the desired state and manages Pods replication and updates.  
- **Service:** An abstraction that exposes Pods as a network service.  
- **Namespace:** A virtual cluster to isolate resources within a cluster.  
- **ConfigMap & Secrets:** Store configuration and sensitive data for Pods.  

---

## How Kubernetes Works

1. **Containerize Application:** Package your app and dependencies in containers (e.g., Docker).  
2. **Define Manifests:** Write YAML files describing Pods, Deployments, Services, and other resources.  
3. **Deploy to Cluster:** Use `kubectl` CLI or APIs to apply manifests to the Kubernetes cluster.  
4. **Kubernetes Scheduler:** Assigns Pods to nodes based on resource availability.  
5. **Self-Healing:** Automatically replaces failed Pods, restarts containers, and manages scaling.  
6. **Load Balancing:** Distributes traffic across Pods via Services.  

---

## Getting Started with Kubernetes

### 1. Set Up a Cluster

- Use managed Kubernetes services like **Amazon EKS**, **Google GKE**, **Azure AKS**, or install your own with **kubeadm** or **minikube** for local testing.

### 2. Install kubectl

- Command-line tool to interact with your Kubernetes cluster.

### 3. Write Deployment YAML

Example for a simple nginx deployment:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80

### 4. Apply Deployment
  kubectl apply -f deployment.yaml

### 5. Expose Deployment
kubectl expose deployment nginx-deployment --type=LoadBalancer --port=80
