# 🧠 Volume-based ConfigMap

👉 This method mounts a ConfigMap as a directory inside the container. Each key in the ConfigMap becomes a file in that directory.

📌 **Usage:** When you have large configuration files (like `nginx.conf` or `application.properties`).

### 🧪 STEP 1: Create a ConfigMap with a file
📄 `config-file.yaml`
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: special-config
data:
  config.txt: |
    color=blue
    mode=high-security
    theme=dark
```

### 🧪 STEP 2: Mount as Volume in Pod
📄 `pod-vol-cm.yaml`
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: cm-volume-pod
spec:
  containers:
  - name: my-app
    image: busybox
    command: ["sh", "-c", "cat /etc/config/config.txt; sleep 3600"]
    volumeMounts:
    - name: config-vol
      mountPath: /etc/config
  volumes:
  - name: config-vol
    configMap:
      name: special-config
```

▶ **Apply it**
```bash
kubectl apply -f config-file.yaml
kubectl apply -f pod-vol-cm.yaml
```

🔍 **STEP 3: Verify File Content**
```bash
kubectl exec cm-volume-pod -- ls /etc/config
kubectl exec cm-volume-pod -- cat /etc/config/config.txt
```

🧠 **PRO TIP:** Changes to the ConfigMap will eventually (after a minute or two) sync to the file inside the pod **without** a restart!

🧹 **STEP 4: Clean Up**
```bash
kubectl delete -f pod-vol-cm.yaml
```
