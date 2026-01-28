# 🧠 LoadBalancer Service

👉 A LoadBalancer service is the standard way to expose a service to the **internet** when using a Cloud Provider (AWS, GCP, Azure).

📌 **How it works:**
1. K8s requests a Load Balancer from the cloud provider (e.g., AWS NLB/ALB).
2. The Cloud Provider gives K8s an External IP/DNS.
3. Traffic goes from the Internet -> Cloud Balancer -> NodePort -> Pod.

### 🧪 STEP 1: Create a LoadBalancer
📄 `loadbalancer.yaml`
```yaml
apiVersion: v1
kind: Service
metadata:
  name: cloud-svc
spec:
  type: LoadBalancer
  selector:
    app: my-web-app
  ports:
  - port: 80
    targetPort: 80
```

▶ **Apply it**
```bash
kubectl apply -f loadbalancer.yaml
```

🔍 **STEP 2: Get External IP**
```bash
kubectl get svc cloud-svc
```
Wait until `EXTERNAL-IP` changes from `<pending>` to a real IP/DNS.

⚠️ **Note:** If you are on Minikube, run `minikube tunnel` in a separate terminal to see the external IP.

🧠 **COMPARE TYPES**
| Type | Best For |
| :--- | :--- |
| **ClusterIP** | Internal traffic only. |
| **NodePort** | Direct node access (dev/test). |
| **LoadBalancer** | Production traffic from Internet (Cloud). |

🧹 **STEP 3: Clean Up**
```bash
kubectl delete svc cloud-svc
```
