# 🧠 Namespaces

👉 Namespaces are virtual clusters within a single physical cluster. They provide isolation.

### 🧪 Use Cases:
- Separating Environments: `dev`, `staging`, `prod`.
- Team Isolation: `team-a`, `team-b`.

### 🔍 Explore Namespaces:
```bash
kubectl get namespaces
```

▶ **Create a Namespace:**
```bash
kubectl create namespace my-app
```

▶ **Run a Pod in a specific Namespace:**
```bash
kubectl apply -f pod.yaml -n my-app
```

📌 **Default Namespaces:**
- `default`: Where things go if you don't specify.
- `kube-system`: For K8s system components.
- `kube-public`: Visible to everyone.
