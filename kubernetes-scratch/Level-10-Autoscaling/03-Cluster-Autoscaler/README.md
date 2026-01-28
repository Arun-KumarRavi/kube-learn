# 🧠 Cluster Autoscaler

👉 Cluster Autoscaler automatically **adds or removes Nodes** from your cluster.

📌 **The Workflow:**
1. A Pod is created but cannot be scheduled because there are **no resources** left on any node.
2. Cluster Autoscaler notices the `Pending` pod.
3. It talks to the Cloud Provider (AWS ASG, GCP Instance Group) and says "Add a node!".
4. Conversely, if a node is underutilized for a long time, it removes it to save money.

### 🧪 Visualization
```text
Pods Need Space -> Scaling Up Nodes -> Cluster Grows 📈
Nodes Are Empty -> Scaling Down Nodes -> Cluster Shrinks 📉
```

🔍 **Check for it:**
Usually installed as a deployment in the `kube-system` namespace.
```bash
kubectl get pods -n kube-system | grep autoscaler
```

🧠 **KEY CONCEPT**
Cluster Autoscaler manages **Infra**, while HPA manages **Workload**. They work together perfectly!
