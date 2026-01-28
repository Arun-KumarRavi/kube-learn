# 🧠 Affinity and Anti-Affinity

👉 Affinity and Anti-Affinity provide more complex and flexible pod placement rules than simple NodeSelectors.

### 1. **Pod Affinity**
"I want this pod to run **near** (on the same node/zone) as these other pods." 
*Example: Run Cache near Web-app for low latency.*

### 2. **Pod Anti-Affinity**
"I want this pod to run **away from** these other pods."
*Example: Don't run two database replicas on the same node (for high availability).*

### 🧪 STEP 1: Create a Pod with Anti-Affinity
📄 `anti-affinity.yaml`
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ha-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: web
  template:
    metadata:
      labels:
        app: web
    spec:
      affinity:
        podAntiAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
          - labelSelector:
              matchExpressions:
              - key: app
                operator: In
                values:
                - web
            topologyKey: "kubernetes.io/hostname"
      containers:
      - name: nginx
        image: nginx
```

🧠 **KEY TERMS**
- `requiredDuringScheduling`: Hard requirement (must be met).
- `preferredDuringScheduling`: Soft requirement (best effort).
- `topologyKey`: The scope. Usually `hostname` (separate node) or `zone`.

🧹 **STEP 2: Clean Up**
```bash
kubectl delete deployment ha-app
```
