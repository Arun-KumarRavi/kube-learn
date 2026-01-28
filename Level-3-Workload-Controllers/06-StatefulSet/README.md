# 🧠 StatefulSet

👉 StatefulSet is the workload API object used to manage **stateful applications**.

📌 **Deployment vs StatefulSet:**
- **Deployment:** For stateless apps (like Web APIs). Pods are interchangeable and have random names (e.g., `web-789f`).
- **StatefulSet:** For stateful apps (like Databases - MongoDB, MySQL, Redis). Pods have a fixed identity and stable network names (e.g., `db-0`, `db-1`).

### 🧪 STEP 1: Create a StatefulSet
📄 `statefulset.yaml`
```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: web-db
spec:
  serviceName: "nginx"
  replicas: 2
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
        image: nginx
        volumeMounts:
        - name: www
          mountPath: /usr/share/nginx/html
  volumeClaimTemplates:
  - metadata:
      name: www
    spec:
      accessModes: [ "ReadWriteOnce" ]
      resources:
        requests:
          storage: 1Gi
```

▶ **Apply it**
```bash
kubectl apply -f statefulset.yaml
```

🔍 **STEP 2: Observe Behavior**
```bash
kubectl get pods
```
Notice the names: `web-db-0` and `web-db-1`. They are created one by one, not all at once!

🧠 **KEY FEATURES**
- **Stable Network ID:** `hostname` is fixed.
- **Stable Storage:** If `web-db-0` dies and restarts, it reconnects to the SAME PersistentVolume it had before.
- **Ordered Deployment:** Pods are started/stopped in a specific order (0, 1, 2...).

🧹 **STEP 3: Clean Up**
```bash
kubectl delete statefulset web-db
```
