# 🧠 Worker Node Components

👉 These are the machines where your applications (containers) actually run.

### 1. **Kubelet**
An agent that runs on each node in the cluster. It makes sure that containers are running in a Pod.
- *Analogy:* The supervisor on the factory floor.

### 2. **Kube-proxy**
A network proxy that runs on each node, implementing part of the K8s Service concept.
- *Analogy:* The traffic cop directing networking traffic.

### 3. **Container Runtime**
The software responsible for running containers (like Docker, containerd, or CRI-O).
- *Analogy:* The actual engine of the car.

🔍 **Inspect your nodes:**
```bash
kubectl describe node <node-name>
```
Look for:
- `Kubelet Version`
- `Container Runtime Version`
- `Addresses`
