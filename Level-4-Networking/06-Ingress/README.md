# 🧠 Ingress and Ingress Controller

👉 **Ingress:** A set of rules that allow external traffic to reach cluster services.
👉 **Ingress Controller:** The "Engine" that carries out those rules (e.g., Nginx, Traefik, Kong).

📌 **Ingress vs LoadBalancer:**
- **LoadBalancer Service:** One cloud LB per service (Expensive!).
- **Ingress:** One cloud LB for **many** services (Smart routing based on Host or Path).

### 🧪 STEP 1: Create an Ingress Rule
📄 `ingress.yaml`
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-app-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - host: myapp.com
    http:
      paths:
      - path: /shop
        pathType: Prefix
        backend:
          service:
            name: shop-service
            port:
              number: 80
      - path: /pay
        pathType: Prefix
        backend:
          service:
            name: payment-service
            port:
              number: 80
```

▶ **Apply it**
```bash
kubectl apply -f ingress.yaml
```

🔍 **STEP 2: Observe**
```bash
kubectl get ingress
```

🧠 **HOW IT WORKS:**
The **Ingress Controller** watches for these objects and automatically updates its configuration (like an Nginx config file) to route traffic appropriately.

🧹 **STEP 3: Clean Up**
```bash
kubectl delete ingress my-app-ingress
```
