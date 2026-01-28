# 🧠 NodePort Service

👉 NodePort exposes the service on a static port on each Node's IP.

📌 **Usage:** Quick development/testing to access apps from outside the cluster.

### 🧪 STEP 1: Create a NodePort Service
📄 `nodeport-demo.yaml`
```yaml
apiVersion: v1
kind: Service
metadata:
  name: web-external
spec:
  type: NodePort
  selector:
    app: my-app
  ports:
  - port: 80
    targetPort: 80
    nodePort: 30007
```

▶ **Apply it**
```bash
kubectl apply -f nodeport-demo.yaml
```

🔍 **STEP 2: Access it**
Find your Node IP: `kubectl get nodes -o wide`
Access at: `http://<NODE-IP>:30007`

🧠 **KEY RANGE**
NodePort default range is **30000-32767**.

🧹 **STEP 3: Clean Up**
```bash
kubectl delete svc web-external
```
