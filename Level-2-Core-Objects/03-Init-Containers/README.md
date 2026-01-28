# 🧠 Init Containers

👉 Init containers run **before** the main containers in a Pod. They must complete successfully before the app containers start.

📌 **Use Cases:**
- Waiting for a service (DB) to be ready.
- Downloading configuration or secrets.
- Setting up filesystem permissions.

### 🧪 STEP 1: Create an Init Container Pod
📄 `init-pod.yaml`
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: init-demo
spec:
  initContainers:
  - name: install-plugin
    image: busybox
    command: ["sh", "-c", "echo 'Installing plugin...' && sleep 10"]
  containers:
  - name: main-app
    image: nginx
```

▶ **Apply it**
```bash
kubectl apply -f init-pod.yaml
```

🔍 **STEP 2: Watch Status changes**
```bash
kubectl get pods -w
```
Status moves from: `Init:0/1` -> `PodInitializing` -> `Running`.

🧠 **KEY FIELDS**
- `initContainers`: Defined at the same level as `containers`.
- **Restart Policy:** If an init container fails, the Pod is restarted until it succeeds (unless `restartPolicy` is Never).

🧹 **STEP 3: Clean Up**
```bash
kubectl delete pod init-demo
```
