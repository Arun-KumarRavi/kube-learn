# 🧠 ReplicaSet (Under the Hood)

👉 A ReplicaSet ensures that a specified number of pod replicas are running at any given time.

📌 **Note:** You usually manage ReplicaSets via **Deployments**.

### 🧪 STEP 1: Create a ReplicaSet
📄 `replicaset.yaml`
```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: my-rs
spec:
  replicas: 3
  selector:
    matchLabels:
      app: web
  template:
    metadata:
      labels:
        app: web
    spec:
      containers:
      - name: nginx
        image: nginx
```

▶ **Apply it**
```bash
kubectl apply -f replicaset.yaml
```

🔍 **STEP 2: Observe Behavior**
```bash
kubectl get rs
kubectl get pods
```
You should see 3 pods running.

🧪 **STEP 3: Test Self-Healing**
Delete one pod manually and watch K8s recreate it instantly!
```bash
kubectl delete pod <pod-name-from-rs>
kubectl get pods
```

🧠 **KEY FIELDS**
| Field | Meaning |
| :--- | :--- |
| `replicas` | Desired number of pods. |
| `selector` | How it finds which pods to manage. |
| `template` | The blueprint for creating new pods. |

🧹 **STEP 4: Clean Up**
```bash
kubectl delete rs my-rs
```
