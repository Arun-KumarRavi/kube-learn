# 🧠 kubectl Basics

👉 `kubectl` is the command-line tool used to communicate with the Kubernetes API server.

📌 **The Syntax:**
`kubectl <command> <type> <name> <flags>`

### 🧪 Common Tasks
- **Get Resources:**
  `kubectl get pods`
- **Describe for Detail:**
  `kubectl describe pod <pod-name>`
- **Check Logs:**
  `kubectl logs <pod-name>`
- **Execute in Container:**
  `kubectl exec -it <pod-name> -- bin/sh`

▶ **Apply a configuration:**
`kubectl apply -f file.yaml`

🧹 **Delete a resource:**
`kubectl delete -f file.yaml`

🧠 **PRO TIP:** 
Use `kubectl explain pod` to see documentation for any field in a YAML file!
