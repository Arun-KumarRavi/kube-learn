# 🧠 Annotations

👉 Annotations are key-value pairs used to attach **arbitrary non-identifying metadata** to objects.

📌 **Labels vs Annotations:**
- **Labels:** Used for selecting/grouping objects (e.g., `env=prod`). K8s uses these internally.
- **Annotations:** Used for external tools, documentation, or metadata (e.g., "created by Jenkins", "owner contact"). K8s does NOT use these to select objects.

### 🧪 STEP 1: Create a Pod with Annotations
📄 `annotations-pod.yaml`
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: annotated-pod
  annotations:
    build-version: "v1.2.3"
    owner: "DevOps-Team"
    description: "This is a test pod for metadata demo"
spec:
  containers:
  - name: nginx
    image: nginx
```

▶ **Apply it**
```bash
kubectl apply -f annotations-pod.yaml
```

🔍 **STEP 2: Observe**
```bash
kubectl describe pod annotated-pod
```
Look for the `Annotations:` section in the output.

🧠 **USE CASES**
- Storing Git commit hashes.
- Configuration for Ingress controllers (e.g., `nginx.ingress.kubernetes.io/rewrite-target`).
- Contact info for the person responsible for the pod.

🧹 **STEP 3: Clean Up**
```bash
kubectl delete pod annotated-pod
```
