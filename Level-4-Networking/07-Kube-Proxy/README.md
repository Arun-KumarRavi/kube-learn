# 🧠 kube-proxy

👉 kube-proxy is a network proxy that runs on each node in your cluster. It is responsible for making "Services" work.

📌 **The Job:**
When you try to talk to a Service IP (ClusterIP), kube-proxy ensures that the traffic actually gets to the right Pod IP.

### 🧪 How it works (IPtables mode)
1. You create a Service.
2. kube-proxy updates "IPtables" rules on every node.
3. When a packet hits the Node, IPtables "catches" it and redirects it to a Pod.

🔍 **Check kube-proxy Pods:**
```bash
kubectl get pods -n kube-system -l k8s-app=kube-proxy
```

🧠 **MODES**
- **IPtables (Default):** Reliable and fast.
- **IPVS:** Better for very large clusters with thousands of services.

📌 **Key Point:** 
Without kube-proxy, Service IPs wouldn't exist and you'd have to talk to Pod IPs directly (which change all the time!).
