# 🧠 StorageClass (Dynamic Provisioning)

👉 A StorageClass allows storage to be created **on-demand** (Dynamically) when a user requests it.

📌 **Static vs Dynamic:**
- **Static:** Admin creates PVs manually (Level 5 Part 2).
- **Dynamic:** Admin defines a "Template" (StorageClass), and Cloud (AWS/GCP/etc.) creates the PV automatically.

### 🧪 STEP 1: Example StorageClass (AWS EBS)
```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: standard
provisioner: kubernetes.io/aws-ebs
parameters:
  type: gp2
reclaimPolicy: Retain
```

🧠 **RECLAIM POLICIES**
- **Retain:** PV is kept after PVC is deleted (Manual cleanup).
- **Delete:** PV is deleted when PVC is deleted (Automatic cleanup).

🔍 **Check your cluster's default SC:**
```bash
kubectl get sc
```
Look for `(default)` next to a name.
