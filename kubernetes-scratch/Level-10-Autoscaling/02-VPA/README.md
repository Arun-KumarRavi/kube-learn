# 🧠 VPA (Vertical Pod Autoscaler)

👉 VPA automatically sets the **Resource Requests and Limits** for your pods, so you don't have to guess.

📌 **HPA vs VPA:**
- **HPA:** Adds more Pods (scaling OUT).
- **VPA:** Makes Pods "bigger" (adding more CPU/RAM) (scaling UP).

⚠️ **Wait!** You usually cannot use HPA and VPA together on the same resource (CPU/Memory).

### 🧪 STEP 1: Create a VPA
📄 `vpa.yaml`
```yaml
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
  name: my-app-vpa
spec:
  targetRef:
    apiVersion: "apps/v1"
    kind: Deployment
    name: my-app
  updatePolicy:
    updateMode: "Auto"
```

🔍 **STEP 2: Observe Recommendations**
```bash
kubectl get vpa my-app-vpa
```
VPA will show "Recommended" values for CPU and Memory based on actual usage history.

🧠 **MODES**
- **Off:** Only provides recommendations (Dry Run).
- **Initial:** Only sets resources during pod creation.
- **Auto:** Restarts pods to update their resources (Recommended).
