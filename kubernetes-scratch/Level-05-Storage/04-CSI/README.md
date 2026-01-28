# 🧠 CSI (Container Storage Interface)

👉 CSI is a standard for exposing arbitrary block and file storage systems to containerized workloads.

📌 **The History:** 
Before CSI, storage drivers were built "In-Tree" (hardcoded into K8s source code). This was hard to maintain. CSI allows storage vendors (AWS, GCP, NetApp, etc.) to write a driver ONCE and have it work on any K8s version.

### 🧪 How you see it in K8s
When you run `kubectl get sc` (StorageClass), look at the `PROVISIONER` column.

Example:
- `ebs.csi.aws.com` (AWS)
- `pd.csi.storage.gke.io` (GKE)

🧠 **KEY CAPABILITIES**
- **Dynamic Provisioning:** Auto-create disks.
- **Snapshots:** Take point-in-time backups.
- **Volume Expansion:** Resize a disk without rebooting the pod.

🔍 **Check for CSI Drivers in your cluster:**
```bash
kubectl get csidrivers
```
