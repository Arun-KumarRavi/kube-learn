# 🧠 Liveness Probe

👉 A Liveness Probe tells K8s if your container is **alive** or dead.

📌 **If it fails:** K8s kills the container and restarts it according to the `restartPolicy`.

### 🧪 STEP 1: Create a Pod with Liveness Probe
📄 `liveness-pod.yaml`
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: liveness-exec
spec:
  containers:
  - name: liveness
    image: busybox
    args:
    - /bin/sh
    - -c
    - touch /tmp/healthy; sleep 30; rm -rf /tmp/healthy; sleep 600
    livenessProbe:
      exec:
        command:
        - cat
        - /tmp/healthy
      initialDelaySeconds: 5
      periodSeconds: 5
```

▶ **Apply it**
```bash
kubectl apply -f liveness-pod.yaml
```

🔍 **STEP 2: Wait 30 seconds**
The file `/tmp/healthy` will be deleted. The probe will fail.
```bash
kubectl get pods -w
```
You'll see `RESTARTS` increment!

🧠 **KEY FIELDS**
- `initialDelaySeconds`: Wait this long before first check.
- `periodSeconds`: How often to check.
- `failureThreshold`: How many failures before action.
