# 🧠 Kubernetes Architecture

👉 K8s follows a Master-Worker architecture (now called Control Plane and Worker Nodes).

📌 **The Big Picture:**
- The **Control Plane** makes decisions (like scheduling).
- The **Worker Nodes** actually run the applications.

### 🧪 Architecture Visualization
Imagine a shipping port:
- **Control Plane:** The port authority/office (directs where ships go).
- **Worker Nodes:** The actual docks/ships (where the work happens).

🔍 **How they communicate:**
The `kubelet` on the worker node talks to the `API Server` on the Control Plane.

🧠 **KEY COMPONENTS**
| Component | Side | Responsibility |
| :--- | :--- | :--- |
| **API Server** | Control Plane | Gateway for all communication. |
| **etcd** | Control Plane | Key-value store for cluster data. |
| **Kubelet** | Worker Node | Agent that runs on each node. |
| **Container Runtime** | Worker Node | Software that runs containers (e.g., Docker, containerd). |
