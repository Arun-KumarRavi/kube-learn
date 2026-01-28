# Kubernetes Learning Curriculum ☸️🚀

This repository contains a comprehensive, level-based Kubernetes learning journey. Each topic is organized into its own folder with a detailed tutorial following a consistent template (Brain, Examples, Step-by-Step, Keys, and Cleanup).

## 🗺️ Curriculum Map

### 🔹 LEVEL 1: KUBERNETES BASICS
- [What is Kubernetes](Level-01-Basics/01-What-is-Kubernetes)
- [Architecture](Level-01-Basics/02-Architecture)
- [Control Plane Components](Level-01-Basics/03-Control-Plane)
- [Worker Node Components](Level-01-Basics/04-Worker-Nodes)
- [kubectl Basics](Level-01-Basics/05-kubectl-Basics)
- [YAML Fundamentals](Level-01-Basics/06-YAML-Fundamentals)
- [Imperative vs Declarative](Level-01-Basics/07-Imperative-vs-Declarative)
- [Namespaces](Level-01-Basics/08-Namespaces)
- [Installation](Level-01-Basics/09-Installation)

### 🔹 LEVEL 2: CORE OBJECTS
- [Pod (Single-container)](Level-02-Core-Objects/01-Pod)
- [Multi-container Pods](Level-02-Core-Objects/02-Multi-container-Pods)
- [Init Containers](Level-02-Core-Objects/03-Init-Containers)
- [Labels & Selectors](Level-02-Core-Objects/04-Labels-and-Selectors)
- [Annotations](Level-02-Core-Objects/05-Annotations)

### 🔹 LEVEL 3: WORKLOAD CONTROLLERS
- [Replication Controller](Level-03-Workload-Controllers/00-Replication-Controller)
- [ReplicaSet](Level-03-Workload-Controllers/01-ReplicaSet)
- [Deployment](Level-03-Workload-Controllers/02-Deployment)
- [DaemonSet](Level-03-Workload-Controllers/03-DaemonSet)
- [Job](Level-03-Workload-Controllers/04-Job)
- [CronJob](Level-03-Workload-Controllers/05-CronJob)
- [StatefulSet](Level-03-Workload-Controllers/06-StatefulSet)

### 🔹 LEVEL 4: NETWORKING & SERVICES
- [ClusterIP Service](Level-04-Networking/01-ClusterIP)
- [NodePort Service](Level-04-Networking/02-NodePort)
- [LoadBalancer Service](Level-04-Networking/03-LoadBalancer)
- [Endpoints](Level-04-Networking/04-Endpoints)
- [CoreDNS](Level-04-Networking/05-CoreDNS)
- [Ingress & Ingress Controller](Level-04-Networking/06-Ingress)
- [kube-proxy](Level-04-Networking/07-Kube-Proxy)

### 🔹 LEVEL 5: STORAGE
- [Volumes (Basic)](Level-05-Storage/01-Volumes-Basic)
- [PV & PVC (Lifecycle & Binding)](Level-05-Storage/02-PV-and-PVC)
- [StorageClass](Level-05-Storage/03-StorageClass)
- [CSI (Container Storage Interface)](Level-05-Storage/04-CSI)

### 🔹 LEVEL 6: CONFIGURATION & SECRETS
- [ConfigMap](Level-06-Configuration/01-ConfigMap)
- [Secrets](Level-06-Configuration/02-Secrets)
- [Volume-based ConfigMap](Level-06-Configuration/03-Volume-based-ConfigMap)
- [Volume-based Secrets](Level-06-Configuration/04-Volume-based-Secrets)

### 🔹 LEVEL 7: SECURITY & ACCESS
- [AuthN vs AuthZ](Level-07-Security/01-AuthN-vs-AuthZ)
- [RBAC Basics](Level-07-Security/02-RBAC-Basics)
- [ClusterRole & ClusterRoleBinding](Level-07-Security/03-ClusterRole)
- [ServiceAccount](Level-07-Security/04-ServiceAccount)
- [TLS Secrets](Level-07-Security/05-TLS-Secrets)

### 🔹 LEVEL 8: SCHEDULING & NODE CONTROL
- [Resource Requests & Limits](Level-08-Scheduling/01-Resource-Limits)
- [Node Selector](Level-08-Scheduling/02-Node-Selector)
- [Taints and Tolerations](Level-08-Scheduling/03-Taints-and-Tolerations)
- [Affinity and Anti-Affinity](Level-08-Scheduling/04-Affinity-and-Anti-Affinity)

### 🔹 LEVEL 9: RELIABILITY & HEALTH
- [Liveness Probe](Level-09-Health/01-Liveness-Probe)
- [Readiness Probe](Level-09-Health/02-Readiness-Probe)
- [Startup Probe](Level-09-Health/03-Startup-Probe)

### 🔹 LEVEL 10: AUTOSCALING
- [HPA (Horizontal Pod Autoscaler)](Level-10-Autoscaling/01-HPA)
- [VPA (Vertical Pod Autoscaler)](Level-10-Autoscaling/02-VPA)
- [Cluster Autoscaler](Level-10-Autoscaling/03-Cluster-Autoscaler)

---
*Happy Learning!* 🚀
