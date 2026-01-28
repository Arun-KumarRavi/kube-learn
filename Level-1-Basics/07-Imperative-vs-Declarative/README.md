# 🧠 Imperative vs Declarative

👉 There are two ways to manage Kubernetes resources.

### 1. **Imperative (Tell me what to DO)**
You use commands to make changes directly.
- *Command:* `kubectl run nginx --image=nginx`
- *Pros:* Fast, easy for testing.
- *Cons:* No record of changes, hard to automate.

### 2. **Declarative (Tell me what you WANT)**
You define the desired state in a YAML file and K8s makes it happen.
- *Command:* `kubectl apply -f nginx.yaml`
- *Pros:* Versions can be stored in Git (GitOps), repeatable.
- *Cons:* Requires writing YAML.

📌 **In Real Life:** Deeply favor the **Declarative** approach using `kubectl apply`.
