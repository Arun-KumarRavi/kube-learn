# 🧠 Replication Controller (Legacy)

👉 A ReplicationController (RC) ensures that a specified number of pod replicas are running at any one time. 

📌 **Important Note:** This is the **legacy** version of ReplicaSet. In modern Kubernetes, you should use **Deployments** which manage **ReplicaSets**.

### 🧪 STEP 1: Create a Replication Controller
📄 `rc.yaml`
```yaml
apiVersion: v1
kind: ReplicationController
metadata:
  name: my-rc
spec:
  replicas: 2
  selector:
    app: legacy-app
  template:
    metadata:
      labels:
        app: legacy-app
    spec:
      containers:
      - name: nginx
        image: nginx
```

▶ **Apply it**
```bash
kubectl apply -f rc.yaml
```

🔍 **STEP 2: Observe Behavior**
```bash
kubectl get rc
kubectl get pods
```

🧠 **RC vs ReplicaSet (Interview Question)**
| Feature | Replication Controller (RC) | ReplicaSet (RS) |
| :--- | :--- | :--- |
| **Selectors** | Only equality-based (`app: web`) | Equality AND Set-based (`env in (prod, qa)`) |
| **API Version** | `v1` | `apps/v1` |
| **Recommendation** | Legacy / Avoid | Preferred / Standard |

🧹 **STEP 3: Clean Up**
```bash
kubectl delete rc my-rc
```
