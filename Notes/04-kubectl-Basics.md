# Kubernetes Notes
# Chapter 04 - kubectl Basics

> 📘 **Level:** Beginner
> ⏱️ **Estimated Reading Time:** 60–75 minutes
> 🛠️ **Practice Time:** 3–4 hours

---

# 📚 Table of Contents

1. What is kubectl?
2. Why Use kubectl?
3. kubectl Architecture
4. Configure kubectl
5. Cluster Commands
6. Node Commands
7. Pod Commands
8. Deployment Commands
9. Service Commands
10. Namespace Commands
11. ConfigMap & Secret Commands
12. Useful Commands
13. Best Practices
14. Summary
15. Interview Questions
16. Practice Exercises
17. Mini Project
18. Further Reading

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Understand kubectl
- Connect to Kubernetes clusters
- Manage Pods and Deployments
- Work with Services and Namespaces
- Execute common kubectl commands

---

# 📖 What is kubectl?

**kubectl** is the official **Command Line Interface (CLI)** used to interact with Kubernetes clusters.

Using kubectl, you can:

- 📦 Create resources
- 🔍 View resources
- ✏️ Update resources
- ❌ Delete resources
- 📊 Monitor applications
- 📜 View logs

---

# 💡 Why Use kubectl?

Without kubectl:

```text
User

↓

Manual API Calls

↓

Complex Management ❌
```

With kubectl:

```text
User

↓

kubectl Commands

↓

API Server

↓

Cluster Managed ✅
```

Benefits:

- ✅ Easy cluster management
- ✅ Fast deployment
- ✅ Resource monitoring
- ✅ Troubleshooting

---

# 🏗️ kubectl Architecture

```text
kubectl

↓

API Server

↓

Control Plane

↓

Worker Nodes

↓

Pods
```

Every kubectl command communicates with the Kubernetes API Server.

---

# ⚙️ Configure kubectl

View current configuration:

```bash
kubectl config view
```

Display current context:

```bash
kubectl config current-context
```

List all contexts:

```bash
kubectl config get-contexts
```

Switch context:

```bash
kubectl config use-context <context-name>
```

---

# ☸️ Cluster Commands

Display cluster information:

```bash
kubectl cluster-info
```

Display Kubernetes version:

```bash
kubectl version
```

List API resources:

```bash
kubectl api-resources
```

List API versions:

```bash
kubectl api-versions
```

---

# 🖥️ Node Commands

List nodes:

```bash
kubectl get nodes
```

List detailed node information:

```bash
kubectl get nodes -o wide
```

Describe a node:

```bash
kubectl describe node <node-name>
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

Describe a Deployment:

```bash
kubectl describe deployment <deployment-name>
```

Scale a Deployment:

```bash
kubectl scale deployment <deployment-name> --replicas=3
```

Restart a Deployment:

```bash
kubectl rollout restart deployment <deployment-name>
```

Check rollout status:

```bash
kubectl rollout status deployment <deployment-name>
```

---

# 🌐 Service Commands

List Services:

```bash
kubectl get services
```

Describe a Service:

```bash
kubectl describe service <service-name>
```

Expose a Deployment:

```bash
kubectl expose deployment <deployment-name> \
--type=NodePort \
--port=80
```

---

# 🗂️ Namespace Commands

List Namespaces:

```bash
kubectl get namespaces
```

Create Namespace:

```bash
kubectl create namespace dev
```

Delete Namespace:

```bash
kubectl delete namespace dev
```

---

# 🔐 ConfigMap & Secret Commands

List ConfigMaps:

```bash
kubectl get configmaps
```

List Secrets:

```bash
kubectl get secrets
```

Describe a ConfigMap:

```bash
kubectl describe configmap <configmap-name>
```

Describe a Secret:

```bash
kubectl describe secret <secret-name>
```

---

# 🛠️ Useful Commands

Create resources:

```bash
kubectl apply -f app.yaml
```

Delete resources:

```bash
kubectl delete -f app.yaml
```

View all resources:

```bash
kubectl get all
```

Explain resource fields:

```bash
kubectl explain deployment
```

Watch resources continuously:

```bash
kubectl get pods -w
```

---

# 🏗️ kubectl Workflow

```text
Write YAML

↓

kubectl apply

↓

API Server

↓

Control Plane

↓

Worker Node

↓

Pod Running
```

---

# 🏆 Best Practices

- ✅ Use namespaces for organization
- ✅ Store manifests in Git
- ✅ Use `kubectl apply` instead of `create`
- ✅ Verify resources after deployment
- ✅ Use `kubectl describe` for troubleshooting
- ✅ Check logs regularly
- ✅ Learn resource shortcuts (`po`, `svc`, `deploy`)

---

# 🌍 Common Resource Shortcuts

| Full Name | Shortcut |
|-----------|----------|
| pods | po |
| services | svc |
| deployments | deploy |
| namespaces | ns |
| nodes | no |
| configmaps | cm |

Example:

```bash
kubectl get po
```

---

# 📝 Key Takeaways

- kubectl is the Kubernetes CLI.
- It communicates with the API Server.
- It manages every Kubernetes resource.
- It supports creation, update, deletion, and monitoring.
- It is the most commonly used Kubernetes tool.

---

# 📋 Summary

In this chapter, you learned:

- kubectl Basics
- Cluster Commands
- Node Commands
- Pod Commands
- Deployment Commands
- Service Commands
- Namespace Commands
- Useful kubectl Commands

---

# ❓ Interview Questions

## Beginner

1. What is kubectl?
2. Why is kubectl used?
3. What command lists Pods?
4. How do you view cluster information?
5. How do you view logs of a Pod?

---

## Intermediate

6. Explain kubectl architecture.
7. Difference between `apply` and `create`?
8. How do you scale a Deployment?
9. What is the purpose of `kubectl describe`?
10. How do you switch Kubernetes contexts?

---

## Advanced

11. Explain the kubectl workflow.
12. How does kubectl communicate with Kubernetes?
13. How would you troubleshoot a failed Pod?
14. Explain kubectl configuration contexts.
15. What are the most useful kubectl commands for production?

---

# 🎯 Practice Exercises

## Exercise 1

View cluster information.

```bash
kubectl cluster-info
```

---

## Exercise 2

List all Pods.

```bash
kubectl get pods
```

---

## Exercise 3

Create a namespace.

```bash
kubectl create namespace demo
```

---

## Exercise 4

Deploy an application using a YAML file.

```bash
kubectl apply -f app.yaml
```

---

## Exercise 5

View logs of a running Pod.

```bash
kubectl logs <pod-name>
```

---

# 🧩 Mini Project

Create a Markdown file named:

```text
kubectl-cheatsheet.md
```

Include:

- Cluster Commands
- Pod Commands
- Deployment Commands
- Service Commands
- Namespace Commands
- Useful kubectl Commands

Commit it to Git:

```bash
git add .
git commit -m "Add kubectl basics guide"
```

---

# 📚 Further Reading

- Kubernetes Documentation
- kubectl Cheat Sheet
- Kubernetes API Reference
- Kubernetes CLI Documentation

---

# 📚 Navigation

| ⬅️ Previous | 🏠 Home | ➡️ Next |
|------------|---------|---------|
| [03 - Installing Kubernetes](03-Installing-Kubernetes.md) | [Kubernetes Roadmap](README.md) | [05 - Pods](05-Pods.md) |

---

# 🚀 What's Next?

In **Chapter 05 – Pods**, you'll learn:

- 📦 What is a Pod?
- 🏗️ Pod Architecture
- 📝 Pod YAML
- 🚀 Creating Pods
- 🔄 Pod Lifecycle
- 📊 Managing Pods
- 🛠️ Pod Best Practices
