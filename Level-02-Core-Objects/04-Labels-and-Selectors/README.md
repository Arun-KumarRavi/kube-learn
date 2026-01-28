# 🧠 Labels and Selectors

👉 **Labels** are key-value pairs attached to objects (like Pods).
👉 **Selectors** are used by controllers (like Services or Deployments) to find and "group" objects with specific labels.

📌 **Think of it like:**
- **Labels:** Tags on a shirt.
- **Selectors:** "Give me all shirts that have the tag 'Red'".

### 🧪 STEP 1: Create Labeled Pods
📄 `labeled-pods.yaml`
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-frontend
  labels:
    tier: frontend
    env: prod
spec:
  containers:
  - name: nginx
    image: nginx
---
apiVersion: v1
kind: Pod
metadata:
  name: pod-backend
  labels:
    tier: backend
    env: prod
spec:
  containers:
  - name: nginx
    image: nginx
```

▶ **Apply it**
```bash
kubectl apply -f labeled-pods.yaml
```

🔍 **STEP 2: Filter by Labels**
```bash
kubectl get pods -l tier=frontend
kubectl get pods --show-labels
```

🧠 **KEY SELECTOR TYPES**
| Type | Example |
| :--- | :--- |
| **Equality-based** | `tier: frontend` |
| **Set-based** | `env in (prod, dev)` |

🧹 **STEP 3: Clean Up**
```bash
kubectl delete pod -l env=prod
```
