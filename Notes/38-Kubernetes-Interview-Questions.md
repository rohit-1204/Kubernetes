# Kubernetes Notes
# Chapter 38 - Kubernetes Interview Questions

> 📘 **Level:** Beginner to Advanced
> ⏱️ **Estimated Reading Time:** 2–3 hours
> 🛠️ **Practice Time:** 5–8 hours

---

# 📚 Table of Contents

1. Introduction
2. Beginner Questions
3. Intermediate Questions
4. Advanced Questions
5. Scenario-Based Questions
6. Rapid Fire Questions
7. Hands-on Questions
8. HR & DevOps Questions
9. Interview Tips
10. Summary
11. Practice Challenge
12. Further Reading

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Prepare for Kubernetes interviews
- Answer conceptual questions confidently
- Solve scenario-based problems
- Perform hands-on Kubernetes tasks
- Crack DevOps and Cloud interviews

---

# 📖 Introduction

Kubernetes is one of the most frequently asked technologies in DevOps, Cloud, and Site Reliability Engineering (SRE) interviews.

Interviewers generally evaluate:

- Kubernetes fundamentals
- Architecture
- Networking
- Storage
- Security
- Troubleshooting
- Production experience
- Hands-on knowledge

---

# 🌱 Beginner Interview Questions

### 1. What is Kubernetes?

**Answer:**

Kubernetes is an open-source container orchestration platform used to deploy, scale, and manage containerized applications automatically.

---

### 2. Why is Kubernetes used?

**Answer:**

Kubernetes provides:

- High availability
- Auto scaling
- Self healing
- Service discovery
- Load balancing
- Rolling updates
- Resource management

---

### 3. What is a Pod?

**Answer:**

A Pod is the smallest deployable unit in Kubernetes.

It contains one or more containers that share:

- Network
- Storage
- Lifecycle

---

### 4. What is a Node?

**Answer:**

A Node is a worker machine that runs Pods.

Types:

- Control Plane Node
- Worker Node

---

### 5. What is a Deployment?

**Answer:**

A Deployment manages Pods using ReplicaSets and provides:

- Rolling updates
- Rollbacks
- Scaling
- Self healing

---

### 6. What is a ReplicaSet?

**Answer:**

A ReplicaSet ensures that a specified number of Pod replicas are always running.

---

### 7. Difference between Deployment and ReplicaSet?

| Deployment | ReplicaSet |
|------------|------------|
| Manages ReplicaSets | Manages Pods |
| Supports Rollbacks | No Rollbacks |
| Rolling Updates | No Rolling Updates |
| Recommended | Rarely used directly |

---

### 8. What is kubectl?

**Answer:**

kubectl is the Kubernetes command-line tool used to interact with the cluster.

---

### 9. What is a Namespace?

**Answer:**

Namespaces logically isolate Kubernetes resources within the same cluster.

---

### 10. What is a Service?

**Answer:**

A Service exposes Pods using a stable IP and DNS name.

---

# 🚀 Intermediate Interview Questions

### 11. Explain Kubernetes Architecture.

**Answer:**

The architecture consists of:

- API Server
- etcd
- Scheduler
- Controller Manager
- Worker Nodes
- kubelet
- kube-proxy
- Container Runtime

---

### 12. What is etcd?

**Answer:**

etcd is Kubernetes' distributed key-value database that stores the cluster state.

---

### 13. What is kubelet?

**Answer:**

kubelet runs on every worker node and communicates with the API Server.

It ensures containers are running as expected.

---

### 14. What is kube-proxy?

**Answer:**

kube-proxy manages network rules and enables communication between Services and Pods.

---

### 15. Explain Rolling Updates.

**Answer:**

Rolling Updates replace Pods gradually without downtime.

---

### 16. What are Liveness and Readiness Probes?

| Probe | Purpose |
|--------|---------|
| Liveness | Restarts unhealthy containers |
| Readiness | Controls traffic routing |
| Startup | Handles slow-starting applications |

---

### 17. What is ConfigMap?

**Answer:**

Stores non-sensitive configuration data separately from application code.

---

### 18. What are Secrets?

**Answer:**

Secrets securely store sensitive information like passwords, API keys, and certificates.

---

### 19. Difference between ConfigMap and Secret?

| ConfigMap | Secret |
|------------|---------|
| Plain configuration | Sensitive data |
| Base64 encoding not required | Base64 encoded |
| Non-confidential | Confidential |

---

### 20. Explain Ingress.

**Answer:**

Ingress manages external HTTP/HTTPS traffic to Services using routing rules.

---

# 🔥 Advanced Interview Questions

### 21. Explain Kubernetes Networking.

Topics to mention:

- Pod Networking
- CNI Plugins
- Services
- Ingress
- Network Policies
- DNS

---

### 22. What is RBAC?

RBAC controls access to Kubernetes resources using:

- Roles
- ClusterRoles
- RoleBindings
- ClusterRoleBindings

---

### 23. Explain Horizontal Pod Autoscaler.

HPA automatically scales Pods using metrics such as:

- CPU
- Memory
- Custom metrics

---

### 24. Explain StatefulSet.

StatefulSet manages stateful applications requiring:

- Stable identities
- Persistent storage
- Ordered deployment

---

### 25. Explain DaemonSet.

DaemonSet ensures one Pod runs on every node.

Common examples:

- Fluent Bit
- Node Exporter
- Monitoring agents

---

### 26. Explain Helm.

Helm is Kubernetes' package manager.

It deploys applications using reusable Charts.

---

### 27. What is Kustomize?

Kustomize customizes Kubernetes YAML without templates.

---

### 28. Explain Kubernetes Security.

Mention:

- RBAC
- Network Policies
- Secrets
- Pod Security Standards
- Image Scanning
- TLS

---

### 29. Explain Kubernetes Scheduling.

Scheduler selects an appropriate node based on:

- Resources
- Affinity
- Taints
- Tolerations
- Constraints

---

### 30. Explain Kubernetes Self-Healing.

Kubernetes automatically:

- Restarts failed Pods
- Reschedules Pods
- Maintains desired replicas

---

# 💼 Scenario-Based Interview Questions

### Scenario 1

A Pod is stuck in **Pending** state.

How would you troubleshoot it?

**Answer:**

- Check events
- Verify node resources
- Inspect scheduler messages
- Check node selectors
- Verify taints and tolerations

---

### Scenario 2

Pods are running but application isn't accessible.

What would you check?

- Service
- Endpoints
- Ingress
- Labels
- Target Port
- Application logs

---

### Scenario 3

Pods keep restarting.

Possible reasons:

- CrashLoopBackOff
- Failed health checks
- Out of memory
- Application bugs

---

### Scenario 4

High CPU usage.

Possible solutions:

- HPA
- Resource limits
- Optimize application
- Scale nodes

---

### Scenario 5

Production deployment failed.

Steps:

- Check rollout status
- View logs
- Describe Deployment
- Rollback if required

---

# ⚡ Rapid Fire Questions

- What is kubeadm?
- What is Minikube?
- What is kubeconfig?
- What is kubelet?
- What is kube-proxy?
- What is CoreDNS?
- What is CNI?
- What is CSI?
- What is CRI?
- What is etcd?
- What is Helm?
- What is HPA?
- What is VPA?
- What is Ingress?
- What is Network Policy?

---

# 💻 Hands-on Interview Questions

Practice these commands:

```bash
kubectl get pods

kubectl describe pod nginx

kubectl logs nginx

kubectl exec -it nginx -- bash

kubectl get svc

kubectl get deployments

kubectl rollout status deployment/nginx

kubectl rollout undo deployment/nginx

kubectl get nodes

kubectl top pods
```

---

# 👨‍💼 HR & DevOps Questions

1. Describe your Kubernetes project.
2. What production issues have you resolved?
3. How do you deploy applications?
4. How do you monitor Kubernetes?
5. Explain your CI/CD pipeline.
6. How do you secure clusters?
7. What cloud platform have you used?
8. Have you worked with Helm?
9. Explain a challenging production incident.
10. Why should we hire you?

---

# 🎯 Interview Tips

- ✅ Understand Kubernetes architecture.
- ✅ Practice kubectl daily.
- ✅ Learn YAML thoroughly.
- ✅ Know troubleshooting steps.
- ✅ Explain concepts with real examples.
- ✅ Build projects on Minikube, Kind, or cloud platforms.
- ✅ Practice Helm and Kustomize.
- ✅ Revise networking and security.

---

# 📋 Summary

For Kubernetes interviews, focus on:

- Architecture
- Pods
- Deployments
- Services
- Networking
- Storage
- Security
- Monitoring
- Troubleshooting
- Production Best Practices

---

# 🧩 Practice Challenge

Create a Kubernetes application that includes:

- Deployment
- Service
- ConfigMap
- Secret
- Ingress
- HPA
- RBAC
- Network Policy
- Helm Chart

Deploy it on:

- Minikube
- Amazon EKS
- Azure AKS
- Google GKE

---

# 📚 Further Reading

- Kubernetes Documentation
- CNCF Kubernetes Learning Path
- Kubernetes Cheat Sheet
- Helm Documentation
- kubectl Command Reference

---

# 📚 Navigation

| ⬅️ Previous | 🏠 Home | ➡️ Next |
|------------|---------|---------|
| [37 - Production Best Practices](37-Production-Best-Practices.md) | [Kubernetes Roadmap](README.md) | [39 - Kubernetes CheatSheet](39-Kubernetes-CheatSheet.md) |

---

# 🚀 What's Next?

In **Chapter 39 – Kubernetes CheatSheet**, you'll get a **quick-reference guide** covering:

- 📦 kubectl Commands
- 🚀 Deployments
- 🌐 Services
- 💾 Storage
- 🔐 Security
- 📊 Monitoring
- ⚡ Troubleshooting
- 🎯 Most-Asked Interview Commands

This chapter serves as a handy reference for daily Kubernetes administration and interview preparation.
