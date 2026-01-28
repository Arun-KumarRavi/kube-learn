# 🧠 Startup Probe

👉 A Startup Probe tells K8s when the application has **officially started**.

📌 **Difference from others:** 
- Liveness/Readiness probes are disabled until the Startup probe succeeds.
- Great for "slow-starting" apps (e.g., legacy Java apps taking 2 minutes to boot).

### 🧪 STEP 1: Create a Pod with Startup Probe
📄 `startup-pod.yaml`
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: slow-app
spec:
  containers:
  - name: app
    image: nginx
    startupProbe:
      httpGet:
        path: /index.html
        port: 80
      failureThreshold: 30
      periodSeconds: 10
    livenessProbe:
      httpGet:
        path: /index.html
        port: 80
      periodSeconds: 10
```

🧠 **HOW IT WORKS:** 
The application has `30 * 10 = 300` seconds (5 minutes) to finish its startup. After that, Liveness probes take over.

🔍 **Observe Behavior:**
```bash
kubectl describe pod slow-app
```
Look for `Startup:` in the Events section.

🧹 **STEP 2: Clean Up**
```bash
kubectl delete pod slow-app
```
