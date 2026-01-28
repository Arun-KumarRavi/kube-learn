# 🧠 Job (Run Once / Finite Work)

👉 A Job runs a task to completion.

📌 **Unlike Deployment:**
- Job exits when work is done.
- Pods are NOT restarted forever.

### 🧪 STEP 1: Create a SIMPLE JOB
📄 `job.yaml`
```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: hello-job
spec:
  completions: 1
  backoffLimit: 3
  template:
    spec:
      restartPolicy: Never
      containers:
      - name: hello
        image: busybox
        command: ["sh", "-c", "echo Hello Kubernetes Job && sleep 5"]
```

▶ **Apply it**
```bash
kubectl apply -f job.yaml
```

🔍 **STEP 2: Observe Behavior**
```bash
kubectl get jobs
kubectl get pods
```
Expected: Pod moves to `Completed` status.

📄 **STEP 3: Check Logs**
```bash
kubectl logs job/hello-job
```

🧠 **KEY FIELDS**
| Field | Meaning |
| :--- | :--- |
| `completions` | How many successful runs required. |
| `backoffLimit` | Retry attempts if failure. |
| `restartPolicy` | Must be `Never` or `OnFailure`. |

🧹 **STEP 4: Clean Up**
```bash
kubectl delete job hello-job
```
