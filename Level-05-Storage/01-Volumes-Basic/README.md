# 🧠 Volumes (Basic)

👉 A Volume is a directory, possibly containing some data, which is accessible to the containers in a pod.

📌 **Why Volumes?** Containers are ephemeral. When they restart, data is lost. Volumes solve this.

### 🧪 STEP 1: Create a Pod with emptyDir
📄 `emptydir-pod.yaml`
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: volume-demo
spec:
  containers:
  - name: alpine-1
    image: alpine
    command: ["sh", "-c", "echo 'Hello from Container 1' > /data/hello.txt; sleep 3600"]
    volumeMounts:
    - name: shared-data
      mountPath: /data
  - name: alpine-2
    image: alpine
    command: ["sh", "-c", "sleep 5; cat /data/hello.txt; sleep 3600"]
    volumeMounts:
    - name: shared-data
      mountPath: /data
  volumes:
  - name: shared-data
    emptyDir: {}
```

▶ **Apply it**
```bash
kubectl apply -f emptydir-pod.yaml
```

🔍 **STEP 2: Observe Behavior**
```bash
kubectl logs volume-demo -c alpine-2
```
Expected: `Hello from Container 1`

🧠 **KEY VOLUME TYPES**
| Type | Usage |
| :--- | :--- |
| **emptyDir** | Temporary storage shared between containers in a pod. |
| **hostPath** | Mounts a file/directory from the host node's filesystem. |
| **configMap/Secret** | Mounts K8s objects as files. |

🧹 **STEP 3: Clean Up**
```bash
kubectl delete pod volume-demo
```
