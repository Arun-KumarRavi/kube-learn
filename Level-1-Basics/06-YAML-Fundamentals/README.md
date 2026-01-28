# 🧠 YAML Fundamentals

👉 Kubernetes objects are defined using YAML (Yet Another Markup Language). It is human-readable and indentation-based.

📌 **4 Required Fields in K8s YAML:**
1.  **apiVersion:** Which version of the K8s API to use.
2.  **kind:** What kind of object (Pod, Service, etc.).
3.  **metadata:** Data that helps identify the object (name, labels).
4.  **spec:** What state you want for the object.

### 🧪 Example structure
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
  - name: my-container
    image: nginx
```

⚠️ **Warning:** Spaces matter! Always use 2 spaces for indentation, never tabs.
