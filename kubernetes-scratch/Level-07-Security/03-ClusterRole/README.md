# 🧠 ClusterRole and ClusterRoleBinding

👉 **Role/RoleBinding** are limited to a specific **Namespace**. 
👉 **ClusterRole/ClusterRoleBinding** apply cluster-wide (all namespaces).

📌 **Use Cases:**
- Giving an admin access to everything in the cluster.
- Giving a monitoring tool access to list nodes (which are cluster-scoped, not in a namespace).

### 🧪 STEP 1: Create a ClusterRole
📄 `clusterrole.yaml`
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: secrets-reader-global
rules:
- apiGroups: [""]
  resources: ["secrets"]
  verbs: ["get", "watch", "list"]
```

### 🧪 STEP 2: Create a ClusterRoleBinding
📄 `clusterrolebinding.yaml`
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: global-secret-access
subjects:
- kind: User
  name: "manager-user"
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: ClusterRole
  name: secrets-reader-global
  apiGroup: rbac.authorization.k8s.io
```

▶ **Apply both**
```bash
kubectl apply -f clusterrole.yaml
kubectl apply -f clusterrolebinding.yaml
```

🔍 **STEP 3: Verify Access**
```bash
kubectl auth can-i list secrets --as manager-user --all-namespaces
```
Expected: `yes`

🧠 **KEY DIFFERENCE**
| Scope | Role & RoleBinding | ClusterRole & ClusterRoleBinding |
| :--- | :--- | :--- |
| **Namespace** | Specific (e.g., `dev`) | Cluster-wide (All Namespaces) |
| **Resources** | Namespaced (Pods, Services) | Namespaced AND Cluster-scoped (Nodes, PVs) |

🧹 **STEP 4: Clean Up**
```bash
kubectl delete clusterrolebinding global-secret-access
kubectl delete clusterrole secrets-reader-global
```
