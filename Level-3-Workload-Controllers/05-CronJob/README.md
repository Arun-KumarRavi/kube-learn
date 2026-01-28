# 🧠 CronJob (Scheduled Job)

👉 CronJob = Job on a schedule. Just like Linux cron.

### 🧪 STEP 1: Create a CronJob
📄 `cronjob.yaml`
```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: hello-cron
spec:
  schedule: "*/1 * * * *"
  successfulJobsHistoryLimit: 3
  failedJobsHistoryLimit: 1
  jobTemplate:
    spec:
      template:
        spec:
          restartPolicy: Never
          containers:
          - name: hello
            image: busybox
            command: ["sh", "-c", "date && echo Hello from CronJob"]
```

▶ **Apply it**
```bash
kubectl apply -f cronjob.yaml
```

🔍 **STEP 2: Watch CronJob Run**
```bash
kubectl get cronjobs
# Wait 1 minute
kubectl get jobs
```

🧠 **CRON FORMAT**
```text
*  *  *  *  *
│  │  │  │  │
│  │  │  │  └─ Day of week
│  │  │  └──── Month
│  │  └─────── Day of month
│  └────────── Hour
└───────────── Minute
```

🧹 **STEP 3: Clean Up**
```bash
kubectl delete cronjob hello-cron
```
