# 🧠 TLS Secrets

👉 TLS Secrets are specialized Secrets used to store SSL/TLS certificates and private keys.

📌 **Usage:** Securing Ingress controllers (HTTPS).

### 🧪 STEP 1: Create a TLS Secret
📄 `tls-secret.yaml`
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-app-tls
type: kubernetes.io/tls
data:
  tls.crt: <base64-encoded-cert>
  tls.key: <base64-encoded-key>
```

*(Or use imperative command: `kubectl create secret tls my-app-tls --cert=path/to/cert --key=path/to/key`)*

### 🧪 STEP 2: Use in an Ingress
📄 `ingress-https.yaml`
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: secured-ingress
spec:
  tls:
  - hosts:
    - myapp.com
    secretName: my-app-tls
  rules:
  - host: myapp.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: my-app-svc
            port:
              number: 80
```

🧠 **WHY TYPE=TLS?**
K8s ensures that the secret contains exactly two keys: `tls.crt` and `tls.key`. This helps prevent configuration errors.

🧹 **STEP 3: Clean Up**
```bash
kubectl delete secret my-app-tls
```
