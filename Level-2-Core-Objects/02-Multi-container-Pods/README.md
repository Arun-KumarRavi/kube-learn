# 🧠 Multi-container Pods

👉 Kubernetes allows multiple containers inside a single Pod. They share the same Network namespace (IP) and Storage volumes.

📌 **Use Case: Sidecar Pattern**
- **Main Container:** Web server.
- **Sidecar Container:** Log collector or proxy.

### 🧪 STEP 1: Create a Multi-container Pod
📄 `multi-container.yaml`
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: sidecar-pod
spec:
  containers:
  - name: main-app
    image: busybox
    command: ["sh", "-c", "while true; do echo 'Hello from main' >> /var/log/app.log; sleep 5; done"]
    volumeMounts:
    - name: shared-logs
      mountPath: /var/log
  - name: sidecar-log-reader
    image: busybox
    command: ["sh", "-c", "tail -f /var/log/app.log"]
    volumeMounts:
    - name: shared-logs
      mountPath: /var/log
  volumes:
  - name: shared-logs
    emptyDir: {}
```

▶ **Apply it**
```bash
kubectl apply -f multi-container.yaml
```

🔍 **STEP 2: Observe Behavior**
```bash
kubectl get pods
```
Notice: `sidecar-pod  2/2  Running` (Indicates 2 containers running).

📄 **STEP 3: Check Logs of Specific Container**
```bash
kubectl logs sidecar-pod -c sidecar-log-reader
```

🧠 **KEY CONCEPT**
Containers in the same Pod can talk to each other via `localhost`.

🧹 **STEP 4: Clean Up**
```bash
kubectl delete pod sidecar-pod
```
