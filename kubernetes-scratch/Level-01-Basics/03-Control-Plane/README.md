# 🧠 Control Plane Components

👉 These are the "brains" of Kubernetes. They manage the state of the cluster.

### 1. **kube-apiserver**
The entry point for everyone (kubectl, users, nodes).
- *Analogy:* The receptionist and security guard.

### 2. **etcd**
A consistent and highly-available key-value store. This is the cluster's database.
- *Analogy:* The "Source of Truth" notebook.

### 3. **kube-scheduler**
Watches for newly created Pods and selects a node for them to run on.
- *Analogy:* The logistics manager who assigns rooms.

### 4. **kube-controller-manager**
Runs controller processes (Node controller, Job controller, etc.).
- *Analogy:* The manager who ensures everything matches the plan.

🔍 **Check them in a cluster:**
```bash
kubectl get pods -n kube-system
```
(Look for pods starting with `kube-apiserver`, `etcd`, etc.)
