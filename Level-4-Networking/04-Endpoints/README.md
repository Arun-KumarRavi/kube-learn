# 🧠 Endpoints

👉 Endpoints are the glue between a **Service** and its **Pods**.

📌 **The Hidden Logic:**
When you create a Service with a selector, Kubernetes automatically creates an **Endpoints** object with the same name. This object tracks the IP addresses of the Pods that match the selector.

### 🧪 STEP 1: Check Endpoints for an existing service
```bash
kubectl get endpoints
```

🔍 **STEP 2: Deep Dive**
```bash
kubectl describe endpoints <service-name>
```
You will see a list of IP addresses. These are the IPs of your Pods.

🧠 **USE CASE: Manual Endpoints**
If you want a Service to point to an external database (outside K8s), you can create a Service **without** a selector and manually create an Endpoints object pointing to the external IP.

### 🧪 Manual Example
```yaml
apiVersion: v1
kind: Endpoints
metadata:
  name: external-db
subsets:
  - addresses:
      - ip: 10.0.0.1
    ports:
      - port: 3306
```
(Matching Service name `external-db` would then route traffic to that IP).
