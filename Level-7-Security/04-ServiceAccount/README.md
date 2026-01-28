# 🧠 ServiceAccount

👉 A ServiceAccount provides an identity for processes that run in a Pod.

📌 **User vs ServiceAccount:**
- **Users:** For humans (admins, developers) – managed outside K8s.
- **ServiceAccounts:** For machines (Pods, automation) – managed inside K8s.

### 🧪 STEP 1: Create a ServiceAccount
📄 `sa.yaml`
```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: build-robot
```

### 🧪 STEP 2: Link to RBAC (Give it Permissions)
📄 `sa-rbac.yaml`
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: robot-read-pods
subjects:
- kind: ServiceAccount
  name: build-robot
  namespace: default
roleRef:
  kind: Role
  name: pod-reader # Assumes pod-reader role exists from Part 2
  apiGroup: rbac.authorization.k8s.io
```

### 🧪 STEP 3: Use ServiceAccount in a Pod
📄 `pod-with-sa.yaml`
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: robot-pod
spec:
  serviceAccountName: build-robot
  containers:
  - name: nginx
    image: nginx
```

▶ **Apply it**
```bash
kubectl apply -f sa.yaml
kubectl apply -f sa-rbac.yaml
kubectl apply -f pod-with-sa.yaml
```

🔍 **STEP 4: Verify Identity**
Inside the pod, K8s automatically mounts the token:
```bash
kubectl exec robot-pod -- ls /var/run/secrets/kubernetes.io/serviceaccount/
```

🧠 **KEY FIELDS**
| Field | Meaning |
| :--- | :--- |
| `serviceAccountName` | Field in Pod Spec to assign an identity. |
| `automountServiceAccountToken` | Can be set to `false` if the pod doesn't need to talk to the API. |

🧹 **STEP 5: Clean Up**
```bash
kubectl delete pod robot-pod
kubectl delete sa build-robot
```
