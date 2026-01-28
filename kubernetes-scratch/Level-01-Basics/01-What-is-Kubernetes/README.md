# 🧠 What is Kubernetes?

👉 Kubernetes (K8s) is an open-source container orchestration platform that automates the deployment, scaling, and management of containerized applications.

### Examples:
- Scaling a web server when traffic increases.
- Restarting a container if it crashes.
- Managing rolling updates for a new version of an app.

📌 **Key Points:**
- **Orchestration:** It manages the lifecycle of containers.
- **Portability:** Works on-prem, AWS, GCP, Azure, etc.
- **Self-Healing:** Monitors and replaces failed containers.

### 🧪 Basic Concept Check
Unlike a single Docker container, K8s manages a "cluster" of machines.

#### ▶ Key Commands to explore your cluster:
```bash
kubectl cluster-info
kubectl get nodes
```

🔍 **What you'll see:** 
A list of nodes (machines) that are Part of your Kubernetes ecosystem.

🧠 **KEY TERMS**
| Term | Meaning |
| :--- | :--- |
| **Cluster** | A set of nodes that run containerized apps. |
| **Node** | A worker machine (VM or physical). |
| **Control Plane** | The brain of the cluster. |
