# 🧠 Readiness Probe

👉 A Readiness Probe tells K8s if your container is **ready to accept traffic**.

📌 **If it fails:** The Pod is removed from Service endpoints (No traffic is sent to it), but the container is **NOT** restarted.

### 🧪 STEP 1: Create a Pod with Readiness Probe
📄 `readiness-pod.yaml`
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: read-probe
  labels:
    app: my-app
spec:
  containers:
  - name: my-app
    image: nginx
    readinessProbe:
      httpGet:
        path: /index.html
        port: 80
      initialDelaySeconds: 5
      periodSeconds: 5
```

▶ **Apply it**
```bash
kubectl apply -f readiness-pod.yaml
```

🔍 **STEP 2: Observe Status**
```bash
kubectl get pods
```
If the probe hasn't passed yet, you'll see `READY 0/1`. Once it passes, it becomes `1/1`.

🧠 **PRO TIP:** Use Readiness probes to prevent sending traffic to an app while it's still loading data into cache.
