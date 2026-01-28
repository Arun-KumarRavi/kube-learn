# 🧠 RBAC (Role Based Access Control)

👉 RBAC regulates access to computer or network resources based on the roles of individual users within an enterprise.

📌 **The Trinity of RBAC:**
1. **Role:** What can you do? (Can I read pods?)
2. **Subject:** Who are you? (User, Group, ServiceAccount)
3. **RoleBinding:** Link the Who to the What.

### 🧪 STEP 1: Create a Role
📄 `role.yaml`
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: default
  name: pod-reader
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "watch", "list"]
```

### 🧪 STEP 2: Create a RoleBinding
📄 `rolebinding.yaml`
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: read-pods
  namespace: default
subjects:
- kind: User
  name: "john-doe"
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```

🔍 **Verification Command:**
```bash
kubectl auth can-i get pods --as john-doe
```
Expected: `yes`

🧠 **KEY TERMS**
- **Resources:** pod, service, deployment, etc.
- **Verbs:** get, list, create, update, delete, watch.
