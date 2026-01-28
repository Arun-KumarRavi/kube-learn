# 🧠 Node Selector

👉 Node Selector is the simplest way to constrain a Pod to run on specific Nodes.

📌 **Usage:** Moving database pods to nodes with SSDs, or ML pods to nodes with GPUs.

### 🧪 STEP 1: Label a Node
```bash
kubectl label nodes <node-name> disktype=ssd
```

### 🧪 STEP 2: Create a Pod with nodeSelector
📄 `nodeselector-pod.yaml`
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: ssd-pod
spec:
  containers:
  - name: nginx
    image: nginx
  nodeSelector:
    disktype: ssd
```

▶ **Apply it**
```bash
kubectl apply -f nodeselector-pod.yaml
```

🔍 **STEP 3: Observe**
```bash
kubectl get pod ssd-pod -o wide
```
The pod will only be scheduled if a node matches the label. Otherwise, it stays `Pending`.

🧠 **ADVANCED ALTERNATIVE:** 
For more complex rules (e.g., "In this region but NOT that node"), use **Node Affinity**.

🧹 **STEP 4: Clean Up**
```bash
kubectl delete pod ssd-pod
kubectl label nodes <node-name> disktype-
```
