# 🧠 ClusterIP Service

👉 ClusterIP is the **default** K8s service type. It provides an internal IP only.

📌 **Usage:** Internal communication (e.g., Frontend talking to Backend).

### 🧪 STEP 1: Create a Pod and a ClusterIP
📄 `clusterip-demo.yaml`
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: web-pod
  labels:
    app: my-internal-app
spec:
  containers:
  - name: nginx
    image: nginx
---
apiVersion: v1
kind: Service
metadata:
  name: internal-svc
spec:
  type: ClusterIP
  selector:
    app: my-internal-app
  ports:
  - port: 80
    targetPort: 80
```

▶ **Apply it**
```bash
kubectl apply -f clusterip-demo.yaml
```

🔍 **STEP 2: Observe Behavior**
```bash
kubectl get svc
```
You'll see a `CLUSTER-IP` but **no** `EXTERNAL-IP`.

🧠 **WHY USE IT?**
Security. It keeps your database or internal APIs invisible to the outside world.

🧹 **STEP 3: Clean Up**
```bash
kubectl delete -f clusterip-demo.yaml
```
