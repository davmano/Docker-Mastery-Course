# 7️⃣ Module 7 – Docker + Kubernetes

### 🎯 Objective
Deploy Dockerized applications to a Kubernetes cluster.

---

## ☸️ 7.1 From Docker Image to Kubernetes Pod

Kubernetes uses container images (from Docker or other runtimes) to run containers inside Pods.

Ensure your image is available in a registry (Docker Hub, ECR, etc.).

---

## 📄 7.2 Simple Deployment + Service

`deployment.yaml`:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: flaskapp-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: flaskapp
  template:
    metadata:
      labels:
        app: flaskapp
    spec:
      containers:
        - name: flaskapp
          image: your-dockerhub-username/flaskapp:latest
          ports:
            - containerPort: 5000
```

`service.yaml`:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: flaskapp-service
spec:
  type: NodePort
  selector:
    app: flaskapp
  ports:
    - port: 80
      targetPort: 5000
      nodePort: 30080
```

Apply:

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml

kubectl get pods
kubectl get svc
```

---

## 🧪 7.3 Lab – ConfigMap & Secret

`configmap.yaml`:

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  APP_MODE: "production"
```

`secret.yaml`:

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: db-secret
type: Opaque
data:
  DB_PASSWORD: c2VjcmV0cGFzcw==  # base64("secretpass")
```

Use in Deployment:

```yaml
      env:
        - name: APP_MODE
          valueFrom:
            configMapKeyRef:
              name: app-config
              key: APP_MODE
        - name: DB_PASSWORD
          valueFrom:
            secretKeyRef:
              name: db-secret
              key: DB_PASSWORD
```

---

## 📋 Summary

| Object     | Purpose                      |
|------------|-----------------------------|
| Deployment | Manages Pods & replicas     |
| Service    | Exposes Pods over network   |
| ConfigMap  | Non-sensitive configuration |
| Secret     | Sensitive values            |

---

▶️ **Next:** [`Module 8 – Advanced Topics`](module-08-advanced-topics.md)
