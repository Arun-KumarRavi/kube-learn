# 🧠 Deployment

👉 A Deployment provides declarative updates for Pods and ReplicaSets. It is the most common way to run apps on K8s.

📌 **Features:**
- Rolling Updates (Zero downtime).
- Scaling.
- Rollbacks.

### 🧪 STEP 1: Create a Deployment
📄 `deployment.yaml`
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
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```

▶ **Apply it**
```bash
kubectl apply -f deployment.yaml
```

🔍 **STEP 2: Scale it (Declarative)**
Update the `replicas: 3` to `replicas: 5` in `deployment.yaml`.
```bash
kubectl apply -f deployment.yaml
```

🧪 **STEP 3: Rolling Update (Declarative)**
Update the image to `nginx:1.16.1` in `deployment.yaml`.
```bash
kubectl apply -f deployment.yaml
kubectl rollout status deployment/nginx-deployment
```

📄 **STEP 4: Rollback (Safety first)**
```bash
kubectl rollout undo deployment/nginx-deployment
```

🧹 **STEP 5: Clean Up**
```bash
kubectl delete deployment nginx-deployment
```
