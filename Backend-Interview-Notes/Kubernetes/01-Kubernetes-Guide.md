# 1. Kubernetes — Full Guide

> 🔴 **Level:** Advanced | ✅ **Interview Frequency:** Medium

---

## 🧠 Concept

**Kubernetes (K8s)** is an **orchestrator** — it automatically runs, scales, heals, and manages
many containers across many servers.

Docker runs **one** container; Kubernetes manages **thousands** across a cluster.

---

## 💬 Simple Explanation

If containers are workers, Kubernetes is the **manager** who hires more workers when busy,
replaces sick ones, and makes sure the job always gets done.

---

## 🗺️ Architecture

```
        ┌──────── Control Plane (brain) ────────┐
        │ API Server │ Scheduler │ Controller    │
        │ etcd (cluster data store)              │
        └───────────────┬────────────────────────┘
             ┌───────────┼────────────┐
             ▼           ▼            ▼
          Node 1       Node 2       Node 3   (worker machines)
          [Pods]       [Pods]       [Pods]
```

---

## 📋 Key Objects

| Object | Meaning |
|--------|---------|
| **Pod** | Smallest unit — wraps one (or few) containers |
| **Deployment** | Manages Pods: scaling, rolling updates, self-healing |
| **Service** | Stable network address to reach Pods (load balances) |
| **ConfigMap** | Non-secret config (key-value) |
| **Secret** | Sensitive config (passwords, tokens) |
| **Ingress** | Routes external HTTP traffic to Services |
| **Namespace** | Virtual cluster to group/isolate resources |

```
Ingress → Service → Deployment → Pods → Containers
```

---

## 🧩 Example YAML

```yaml
# Deployment - runs 3 copies of the app
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
spec:
  replicas: 3                     # 3 pods for high availability
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
        - name: myapp
          image: myapp:1.0
          ports:
            - containerPort: 8080
---
# Service - stable access + load balancing across the pods
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  selector:
    app: myapp
  ports:
    - port: 80
      targetPort: 8080
  type: ClusterIP
```

### Common Commands
```bash
kubectl get pods                 # list pods
kubectl get deployments
kubectl apply -f deploy.yaml     # create/update from file
kubectl scale deployment myapp --replicas=5
kubectl logs <pod>
kubectl describe pod <pod>
kubectl delete pod <pod>         # K8s recreates it (self-healing)
```

---

## 📈 Autoscaling

**HPA (Horizontal Pod Autoscaler)** adds/removes Pods based on CPU/memory load.
```bash
kubectl autoscale deployment myapp --min=2 --max=10 --cpu-percent=70
```

---

## 🔑 Service Types
| Type | Use |
|------|-----|
| **ClusterIP** | Internal only (default) |
| **NodePort** | Exposes on each node's port |
| **LoadBalancer** | Cloud load balancer (external) |
| **Ingress** | HTTP routing by path/host |

---

## 🌍 Real-World Use Case
Run a Spring Boot microservice with 3 replicas. If one Pod crashes, K8s restarts it. On Black
Friday, autoscaling adds more Pods; when traffic drops, it removes them.

---

## ❓ Interview Questions
1. What is Kubernetes? Why use it over plain Docker?
2. What is a Pod?
3. Difference between Deployment and Pod?
4. What is a Service? Types of Services?
5. ConfigMap vs Secret?
6. What is Ingress?
7. What is a Namespace?
8. How does self-healing work?
9. What is HPA (autoscaling)?
10. What is a rolling update / rollback?

---

## ✅ Best Practices
- Use Deployments (not bare Pods) for self-healing & scaling.
- Store secrets in Secrets, config in ConfigMaps.
- Set resource **requests/limits** and **liveness/readiness probes**.
- Use namespaces to separate environments.

## ⚠️ Common Mistakes
- Running single Pods without a Deployment.
- Putting passwords in ConfigMaps (use Secrets).
- No health probes → K8s can't detect broken apps.

---

## ⚡ Quick Revision Notes
- K8s orchestrates containers: scaling, healing, load balancing.
- Pod = smallest unit; Deployment manages Pods; Service = stable access.
- ConfigMap = config, Secret = sensitive data, Ingress = HTTP routing.
- HPA autoscales Pods; self-healing restarts failed Pods.

## 🙋 FAQs
**Q: Docker vs Kubernetes?** Docker builds/runs containers; Kubernetes manages many containers across a cluster.

## 📎 References
- kubernetes.io/docs

[⬅ Back to Kubernetes Index](./README.md)

