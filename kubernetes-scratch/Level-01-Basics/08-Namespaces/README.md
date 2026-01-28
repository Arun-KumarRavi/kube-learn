# 🧠 Namespaces

👉 Namespaces are virtual clusters within a single physical cluster. They provide isolation.

### 🧪 Use Cases:
- Separating Environments: `dev`, `staging`, `prod`.
- Team Isolation: `team-a`, `team-b`.

### 🧪 STEP 1: Create a Namespace Declaratively
📄 `namespace.yaml`
```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: my-app
```

▶ **Apply it**
```bash
kubectl apply -f namespace.yaml
```

🔍 **Explore Namespaces:**
```bash
kubectl get namespaces
```

▶ **Run a Pod in a specific Namespace:**
```bash
kubectl apply -f pod.yaml -n my-app
```

📌 **Default Namespaces:**
- `default`: Where things go if you don't specify.
- `kube-system`: For K8s system components.
- `kube-public`: Visible to everyone.
