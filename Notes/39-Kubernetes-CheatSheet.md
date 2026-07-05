# Kubernetes Notes
# Chapter 39 - Kubernetes CheatSheet

> 📘 **Level:** Beginner to Advanced
> ⏱️ **Estimated Reading Time:** 30–45 minutes
> 🛠️ **Purpose:** Daily Kubernetes Quick Reference

---

# 📚 Table of Contents

1. Cluster Commands
2. Pod Commands
3. Deployment Commands
4. Service Commands
5. ConfigMap & Secret Commands
6. Storage Commands
7. Namespace Commands
8. RBAC Commands
9. Autoscaling Commands
10. Troubleshooting Commands
11. YAML Templates
12. Production Checklist
13. Interview Quick Revision
14. Summary

---

# 🎯 Learning Objectives

After completing this chapter, you will have a quick reference for:

- Daily Kubernetes administration
- kubectl commands
- YAML templates
- Troubleshooting
- Production deployments
- Interview preparation

---

# ☸️ Cluster Commands

Check cluster information:

```bash
kubectl cluster-info
```

View Kubernetes version:

```bash
kubectl version
```

List nodes:

```bash
kubectl get nodes
```

Describe a node:

```bash
kubectl describe node <node-name>
```

View all namespaces:

```bash
kubectl get namespaces
```

---

# 📦 Pod Commands

List Pods:

```bash
kubectl get pods
```

List Pods in all namespaces:

```bash
kubectl get pods -A
```

Describe a Pod:

```bash
kubectl describe pod <pod-name>
```

View Pod logs:

```bash
kubectl logs <pod-name>
```

Follow logs:

```bash
kubectl logs -f <pod-name>
```

View previous logs:

```bash
kubectl logs --previous <pod-name>
```

Execute a shell inside a Pod:

```bash
kubectl exec -it <pod-name> -- /bin/bash
```

Delete a Pod:

```bash
kubectl delete pod <pod-name>
```

---

# 🚀 Deployment Commands

List Deployments:

```bash
kubectl get deployments
```

Create Deployment:

```bash
kubectl apply -f deployment.yaml
```

Scale Deployment:

```bash
kubectl scale deployment nginx --replicas=5
```

Update image:

```bash
kubectl set image deployment/nginx nginx=nginx:latest
```

Check rollout:

```bash
kubectl rollout status deployment/nginx
```

Rollback Deployment:

```bash
kubectl rollout undo deployment/nginx
```

Rollout history:

```bash
kubectl rollout history deployment/nginx
```

Delete Deployment:

```bash
kubectl delete deployment nginx
```

---

# 🌐 Service Commands

List Services:

```bash
kubectl get svc
```

Describe Service:

```bash
kubectl describe svc nginx-service
```

View Endpoints:

```bash
kubectl get endpoints
```

Delete Service:

```bash
kubectl delete svc nginx-service
```

---

# 📄 ConfigMap Commands

Create ConfigMap:

```bash
kubectl create configmap app-config \
--from-literal=ENV=production
```

List ConfigMaps:

```bash
kubectl get configmaps
```

Describe ConfigMap:

```bash
kubectl describe configmap app-config
```

Delete ConfigMap:

```bash
kubectl delete configmap app-config
```

---

# 🔑 Secret Commands

Create Secret:

```bash
kubectl create secret generic db-secret \
--from-literal=password=MyPassword123
```

List Secrets:

```bash
kubectl get secrets
```

Describe Secret:

```bash
kubectl describe secret db-secret
```

Delete Secret:

```bash
kubectl delete secret db-secret
```

---

# 💾 Storage Commands

List Persistent Volumes:

```bash
kubectl get pv
```

List Persistent Volume Claims:

```bash
kubectl get pvc
```

Describe PVC:

```bash
kubectl describe pvc app-pvc
```

---

# 🗂️ Namespace Commands

List namespaces:

```bash
kubectl get ns
```

Create namespace:

```bash
kubectl create namespace dev
```

Delete namespace:

```bash
kubectl delete namespace dev
```

Run commands in a namespace:

```bash
kubectl get pods -n dev
```

---

# 🔐 RBAC Commands

List Roles:

```bash
kubectl get roles
```

List ClusterRoles:

```bash
kubectl get clusterroles
```

List RoleBindings:

```bash
kubectl get rolebindings
```

List ClusterRoleBindings:

```bash
kubectl get clusterrolebindings
```

---

# 📈 Autoscaling Commands

List HPAs:

```bash
kubectl get hpa
```

Describe HPA:

```bash
kubectl describe hpa nginx-hpa
```

View resource usage:

```bash
kubectl top pod
```

View node usage:

```bash
kubectl top node
```

---

# 🛠️ Troubleshooting Commands

View events:

```bash
kubectl get events
```

Sort events:

```bash
kubectl get events --sort-by=.metadata.creationTimestamp
```

Describe resource:

```bash
kubectl describe pod <pod-name>
```

View logs:

```bash
kubectl logs <pod-name>
```

Check YAML:

```bash
kubectl get pod <pod-name> -o yaml
```

View all resources:

```bash
kubectl get all
```

---

# 📄 Useful YAML Templates

## Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app
spec:
  replicas: 3
```

---

## Service

```yaml
apiVersion: v1
kind: Service
metadata:
  name: app-service
spec:
  type: ClusterIP
```

---

## ConfigMap

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
```

---

## Secret

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: app-secret
type: Opaque
```

---

## Ingress

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: app-ingress
```

---

# 🚀 Production Checklist

Before deploying to production, verify:

- ✅ Multiple replicas
- ✅ Resource requests & limits
- ✅ Liveness Probe
- ✅ Readiness Probe
- ✅ Startup Probe
- ✅ RBAC enabled
- ✅ Network Policies configured
- ✅ Secrets used (not hardcoded)
- ✅ Monitoring enabled
- ✅ Logging enabled
- ✅ Autoscaling configured
- ✅ Backup strategy defined
- ✅ TLS enabled
- ✅ Container images scanned
- ✅ Rolling update strategy configured

---

# 💼 Interview Quick Revision

Remember these Kubernetes concepts:

| Topic | Key Point |
|--------|-----------|
| Pod | Smallest deployable unit |
| ReplicaSet | Maintains Pod count |
| Deployment | Manages ReplicaSets |
| Service | Stable networking |
| Ingress | HTTP/HTTPS routing |
| ConfigMap | Non-sensitive configuration |
| Secret | Sensitive data |
| PVC | Persistent storage request |
| HPA | Horizontal Pod Autoscaler |
| DaemonSet | One Pod per node |
| StatefulSet | Stateful workloads |
| RBAC | Access control |
| Helm | Package manager |
| Kustomize | YAML customization |
| Network Policy | Controls Pod traffic |

---

# ⚡ Most Frequently Used Commands

```bash
kubectl get pods

kubectl get deployments

kubectl get svc

kubectl describe pod <pod-name>

kubectl logs <pod-name>

kubectl exec -it <pod-name> -- /bin/bash

kubectl apply -f deployment.yaml

kubectl delete -f deployment.yaml

kubectl rollout status deployment/nginx

kubectl rollout undo deployment/nginx

kubectl top pod

kubectl top node

kubectl get events

kubectl cluster-info
```

---

# 📝 Key Takeaways

- Master `kubectl` commands for daily administration.
- Use YAML manifests to manage resources declaratively.
- Monitor clusters proactively.
- Secure workloads using RBAC, Secrets, and Network Policies.
- Practice troubleshooting commands regularly.
- Follow production best practices for reliability and security.

---

# 📋 Summary

This CheatSheet covered:

- Cluster management
- Pods
- Deployments
- Services
- ConfigMaps
- Secrets
- Storage
- RBAC
- Autoscaling
- Troubleshooting
- Production checklist
- Interview revision

Keep this file handy as a quick reference for daily Kubernetes operations and interview preparation.

---

# 🎉 Congratulations!

You have successfully completed the **Kubernetes Notes Series** 🎊

You now have a complete understanding of:

- ✅ Kubernetes Fundamentals
- ✅ Cluster Architecture
- ✅ Workloads
- ✅ Networking
- ✅ Storage
- ✅ Security
- ✅ Monitoring
- ✅ Troubleshooting
- ✅ Production Best Practices
- ✅ Cloud Kubernetes (EKS, AKS, GKE)
- ✅ Helm & Kustomize
- ✅ Interview Preparation

You're now ready to build, deploy, secure, and manage production-grade Kubernetes applications.

---

# 📚 Navigation

| ⬅️ Previous | 🏠 Home | 🎓 Course Complete |
|------------|---------|--------------------|
| [38 - Kubernetes Interview Questions](38-Kubernetes-Interview-Questions.md) | [Kubernetes Roadmap](README.md) | ✅ Congratulations! |

---

# 🚀 Next Learning Path

After Kubernetes, continue with:

1. 🐳 Docker (Advanced)
2. ☁️ AWS DevOps Services
3. ⚙️ Terraform
4. 🔄 GitHub Actions / Jenkins
5. 📊 Prometheus & Grafana
6. 📜 Ansible
7. 🚀 Argo CD (GitOps)
8. 🌐 Istio Service Mesh
9. 🔐 DevSecOps
10. ☁️ Multi-Cloud Kubernetes
