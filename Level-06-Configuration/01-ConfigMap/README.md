# 🧠 ConfigMap

👉 ConfigMaps store non-sensitive data in key-value pairs.

📌 **Usage:** Storing app settings, URLs, or feature flags.

### 🧪 STEP 1: Create a ConfigMap
📄 `configmap.yaml`
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  APP_COLOR: blue
  APP_MODE: production
```

### 🧪 STEP 2: Use in a Pod (Env Var)
📄 `pod-with-cm.yaml`
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: cm-pod
spec:
  containers:
  - name: my-app
    image: busybox
    command: ["sh", "-c", "echo The mode is $MODE; sleep 3600"]
    env:
    - name: MODE
      valueFrom:
        configMapKeyRef:
          name: app-config
          key: APP_MODE
```

▶ **Apply both**
```bash
kubectl apply -f configmap.yaml
kubectl apply -f pod-with-cm.yaml
```

🔍 **STEP 3: Verify**
```bash
kubectl exec cm-pod -- env | grep MODE
```

🧠 **PRO TIP:** You can also mount a ConfigMap as a **volume** to inject entire configuration files into a container.
