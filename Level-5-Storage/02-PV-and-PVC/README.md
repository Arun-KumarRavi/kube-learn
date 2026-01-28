# 🧠 PV and PVC (The Storage Duo)

👉 **PersistentVolume (PV):** A piece of storage in the cluster (the "Hard Drive").
👉 **PersistentVolumeClaim (PVC):** A request for storage by a user (the "Storage Request").

📌 **The Workflow:**
1. Admin creates a PV.
2. User creates a PVC.
3. K8s binds them.
4. Pod uses the PVC.

### 🧪 STEP 1: Create a PV
📄 `pv.yaml`
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: my-pv
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mnt/data"
```

### 🧪 STEP 2: Create a PVC
📄 `pvc.yaml`
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
```

▶ **Apply both**
```bash
kubectl apply -f pv.yaml
kubectl apply -f pvc.yaml
```

🔍 **STEP 3: Check Binding**
```bash
kubectl get pv,pvc
```
Expected: Status `Bound`.

🧠 **PV ↔ PVC BINDING LIFECYCLE**
1. **Provisioning:** Manual (Static) or Automatic (Dynamic).
2. **Binding:** K8s matches a PVC to a suitable PV and binds them.
3. **Using:** The Pod uses the volume defined in the PVC.
4. **Reclaiming:** What happens to the PV when the PVC is deleted?

🧠 **RECLAIM POLICIES**
- **Retain:** PV is kept; data remains but is "Released" (requires manual cleanup).
- **Delete:** PV and actual storage are both deleted automatically.
- **Recycle:** (Legacy) Performs a basic scrub (`rm -rf /vol/*`).

🧠 **KEY FIELD: accessModes**
- **RWO:** ReadWriteOnce (One node)
- **RWX:** ReadWriteMany (Many nodes)
- **ROX:** ReadOnlyMany (Many nodes)
