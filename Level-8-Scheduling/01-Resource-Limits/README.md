# 🧠 Resource Requests and Limits

👉 Kubernetes uses these to manage how much CPU and RAM a container can use.

📌 **The Difference:**
- **Requests:** What the container is "guaranteed" to get. Used for scheduling.
- **Limits:** The maximum the container is "allowed" to consume.

### 🧪 STEP 1: Define Resources in a Pod
📄 `resource-pod.yaml`
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: resource-demo
spec:
  containers:
  - name: heavy-app
    image: nginx
    resources:
      requests:
        memory: "64Mi"
        cpu: "250m"
      limits:
        memory: "128Mi"
        cpu: "500m"
```

▶ **Apply it**
```bash
kubectl apply -f resource-pod.yaml
```

🔍 **STEP 2: Observe**
```bash
kubectl describe pod resource-demo
```

🧠 **CPU UNIT**
`1000m` (millicores) = 1 Virtual CPU Core.
So `250m` is 0.25 of a core.

⚠️ **OOMKilled:** If a container exceeds its memory **Limit**, K8s will kill it!
