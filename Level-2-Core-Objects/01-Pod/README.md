# 🧠 Pod (Single-container)

👉 A Pod is the smallest deployable object in Kubernetes. It represents a single instance of a running process.

📌 **Note:** You rarely create Pods directly (you use Deployments), but understanding them is crucial.

### 🧪 STEP 1: Create a SIMPLE POD
📄 `pod.yaml`
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  labels:
    app: web
spec:
  containers:
  - name: my-nginx
    image: nginx:latest
    ports:
    - containerPort: 80
```

▶ **Apply it**
```bash
kubectl apply -f pod.yaml
```

🔍 **STEP 2: Observe Behavior**
```bash
kubectl get pods
```
Expected: `nginx-pod  1/1  Running  0  10s`

📄 **STEP 3: Check Logs**
```bash
kubectl logs nginx-pod
```

🧠 **KEY POD FIELDS**
| Field | Meaning |
| :--- | :--- |
| `metadata.labels` | Key-value pairs for organization. |
| `spec.containers` | List of containers in the pod. |
| `containerPort` | Port the container is listening on. |

🧹 **STEP 4: Clean Up**
```bash
kubectl delete pod nginx-pod
```
