# 🧠 Kubernetes Installation

👉 There are several ways to get a cluster running on Ubuntu EC2.

### 1. **Minikube**
Single-node local cluster. Great for learning.
- *Command:* `minikube start --driver=docker`

### 2. **Kubeadm**
The standard tool for bootstrapping a production-like cluster. 
- Requires manual setup of Master and Worker nodes.

### 3. **Kind (Kubernetes in Docker)**
Runs K8s clusters using Docker container nodes. Very fast to spin up for CI/CD.
- *Command:* `kind create cluster`

📌 **Which one to use?**
- **Minikube:** Easiest for beginners.
- **Kind:** Best for local testing without VMs.
- **Kubeadm:** Best for learning "The Hard Way" or prod-like setups.
