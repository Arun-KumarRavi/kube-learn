# 🧠 HPA (Horizontal Pod Autoscaler)

👉 HPA automatically scales the number of pods in a deployment based on observed CPU/Memory usage.

📌 **How it works:** 
The HPA controller queries the Metrics Server every 15 seconds to check the load and adjusts the `replicas` field.

### 🧪 STEP 1: Create a Deployment with Resource Limits
*(HPA requires resource requests to work!)*
📄 `webapp-hpa.yaml`
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-scaler
spec:
  replicas: 1
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
        resources:
          requests:
            cpu: "100m"
```

### 🧪 STEP 2: Create the HPA (Declarative)
📄 `hpa.yaml`
```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: web-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: web-scaler
  minReplicas: 1
  maxReplicas: 10
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 50
```

▶ **Apply it**
```bash
kubectl apply -f hpa.yaml
```

🔍 **STEP 3: Observe Scaling**
```bash
kubectl get hpa -w
```

🧠 **REQUIREMENT**
You must have a **Metrics Server** installed in your cluster for HPA to work!

🧹 **STEP 4: Clean Up**
```bash
kubectl delete hpa web-scaler
kubectl delete deployment web-scaler
```
