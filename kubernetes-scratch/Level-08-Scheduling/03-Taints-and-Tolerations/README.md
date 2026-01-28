# 🧠 Taints and Tolerations

👉 Taints and Tolerations allow you to control which pods can be scheduled onto specific nodes.

📌 **The Concept:**
- **Taint:** Applied to a **Node**. It says "I don't want pods here unless they have a key".
- **Toleration:** Applied to a **Pod**. It says "I can handle this taint".

### 🧪 STEP 1: Taint a Node
```bash
kubectl taint nodes <node-name> gpu=true:NoSchedule
```
*Now, NO pod can be scheduled on this node.*

### 🧪 STEP 2: Create a Pod with Toleration
📄 `toleration-pod.yaml`
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: gpu-app
spec:
  containers:
  - name: cuda
    image: nvidia/cuda
  tolerations:
  - key: "gpu"
    operator: "Equal"
    value: "true"
    effect: "NoSchedule"
```

▶ **Apply it**
```bash
kubectl apply -f toleration-pod.yaml
```

🧠 **TAINT EFFECTS**
- `NoSchedule`: Won't schedule new pods.
- `PreferNoSchedule`: Best effort to avoid.
- `NoExecute`: Will evict existing pods that don't tolerate.

🧹 **STEP 3: Clean Up**
```bash
kubectl taint nodes <node-name> gpu-
```
