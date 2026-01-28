# 🧠 Authentication vs Authorization

👉 In Kubernetes, these are two distinct security layers.

📌 **The Workflow:**
1. **Authentication (AuthN):** Who are you? (Identification)
2. **Authorization (AuthZ):** What can you do? (Permissions)
3. **Admission Control:** Is the request valid/allowed?

### 🧪 Comparison Table

| Feature | Authentication (AuthN) | Authorization (AuthZ) |
| :--- | :--- | :--- |
| **Question** | "Who are you?" | "Are you allowed to do this?" |
| **Methods** | Certificates, Tokens, Passwords. | RBAC, ABAC, Webhook. |
| **Example** | Submitting a valid ID card. | Checking if that ID has access to the Server Room. |

🔍 **Check your Auth status:**
```bash
kubectl config view
```
This shows your current "Identity" in the cluster context.

🧠 **KEY POINT:**
Kubernetes does not have a "User" object in its API. Authentication is handled by external systems (Certificates, OIDC, etc.).
