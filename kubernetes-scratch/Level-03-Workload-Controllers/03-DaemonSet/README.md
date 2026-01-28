# 🧠 DaemonSet

👉 A DaemonSet ensures that **all** (or some) Nodes run a copy of a Pod.

📌 **Use Cases:**
- Log collectors (Fluentd, Logstash).
- Monitoring agents (Prometheus Node Exporter).
- Network plugins (Calico).

### 🧪 STEP 1: Create a DaemonSet
📄 `daemonset.yaml`
```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: logger-ds
spec:
  selector:
    matchLabels:
      name: logging-agent
  template:
    metadata:
      labels:
        name: logging-agent
    spec:
      containers:
      - name: logger
        image: busybox
        command: ["sh", "-c", "while true; do echo 'Logging...'; sleep 10; done"]
```

▶ **Apply it**
```bash
kubectl apply -f daemonset.yaml
```

🔍 **STEP 2: Observe Behavior**
```bash
kubectl get ds
kubectl get pods -o wide
```
You will see exactly one pod per node in your cluster.

🧠 **KEY CONCEPT**
If you add a new node to the cluster, the DaemonSet will automatically start a pod on it.

🧹 **STEP 3: Clean Up**
```bash
kubectl delete ds logger-ds
```
