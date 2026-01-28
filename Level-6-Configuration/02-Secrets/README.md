# 🧠 Secrets

👉 Secrets are like ConfigMaps but for sensitive data (Passwords, Keys, Tokens).

⚠️ **Wait!** By default, K8s Secrets are only **Base64 encoded**, NOT encrypted. Use them with care!

### 🧪 STEP 1: Create a Secret (Imperative is easier)
```bash
kubectl create secret generic my-db-secret --from-literal=password=P@ssw0rd123
```

### 🧪 STEP 2: Use in a Pod
📄 `pod-with-secret.yaml`
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: secret-pod
spec:
  containers:
  - name: my-app
    image: busybox
    command: ["sh", "-c", "echo $DB_PASS; sleep 3600"]
    env:
    - name: DB_PASS
      valueFrom:
        secretKeyRef:
          name: my-db-secret
          key: password
```

▶ **Apply it**
```bash
kubectl apply -f pod-with-secret.yaml
```

🔍 **STEP 3: Check manually**
```bash
kubectl get secret my-db-secret -o jsonpath='{.data.password}' | base64 --decode
```

🧹 **STEP 4: Clean Up**
```bash
kubectl delete secret my-db-secret
kubectl delete pod secret-pod
```
