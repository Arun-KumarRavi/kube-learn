# 🧠 CoreDNS

👉 CoreDNS is a flexible, extensible DNS server that serves as the Kubernetes cluster DNS.

📌 **The Benefit:** 
You don't need to remember IP addresses. You can talk to a service by its name. 
Example: `http://my-backend-service` instead of `http://10.96.0.10`.

### 🧪 STEP 1: Explore CoreDNS Pods
```bash
kubectl get pods -n kube-system -l k8s-app=kube-dns
```

🔍 **STEP 2: Test DNS Resolution**
Run a temporary pod and try to resolve a service name:
```bash
kubectl run test-dns --image=busybox:1.28 --restart=Never -- sleep 3600
kubectl exec test-dns -- nslookup kubernetes.default
```

🧠 **DNS PATTERN**
Services follow this pattern:
`<service-name>.<namespace>.svc.cluster.local`

Example: `backend-auth.prod.svc.cluster.local`

📌 **PRO TIP:** 
Most of the time, you just use the short name `backend-auth` if the calling pod is in the same namespace!
