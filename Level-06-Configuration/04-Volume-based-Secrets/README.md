# 🧠 Volume-based Secrets

👉 This allows you to mount Secrets as files. K8s stores these files in memory (`tmpfs`), so they never touch the physical disk of the worker node.

📌 **Usage:** SSH keys, SSL certificates, or API key files.

### 🧪 STEP 1: Create a Secret with a key
📄 `secret-file.yaml`
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: api-key-secret
type: Opaque
data:
  key.txt: YmVzdC1zZWNyZXQtZXZlcgo= # base64 for 'best-secret-ever'
```

### 🧪 STEP 2: Use in a Pod
📄 `pod-vol-secret.yaml`
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: secret-vol-pod
spec:
  containers:
  - name: auth-app
    image: busybox
    command: ["sh", "-c", "cat /etc/keys/key.txt; sleep 3600"]
    volumeMounts:
    - name: secret-vol
      mountPath: /etc/keys
      readOnly: true
  volumes:
  - name: secret-vol
    secret:
      secretName: api-key-secret
```

▶ **Apply it**
```bash
kubectl apply -f secret-file.yaml
kubectl apply -f pod-vol-secret.yaml
```

🔍 **STEP 3: Check manually**
```bash
kubectl exec secret-vol-pod -- cat /etc/keys/key.txt
```

🧠 **SECURITY NOTE:** Always mount secrets as `readOnly: true` to prevent the application from accidentally modifying them.

🧹 **STEP 4: Clean Up**
```bash
kubectl delete -f pod-vol-secret.yaml
```
