# Kubernetes Notes
# Chapter 05 - Pods

> 📘 **Level:** Beginner
> ⏱️ **Estimated Reading Time:** 60–75 minutes
> 🛠️ **Practice Time:** 3–4 hours

---

# 📚 Table of Contents

1. What is a Pod?
2. Why Pods?
3. Pod Architecture
4. Single vs Multi-Container Pods
5. Pod Lifecycle
6. Creating Pods
7. Pod YAML
8. Managing Pods
9. Pod Commands
10. Best Practices
11. Summary
12. Interview Questions
13. Practice Exercises
14. Mini Project
15. Further Reading

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Understand Kubernetes Pods
- Learn Pod architecture
- Create and manage Pods
- Understand the Pod lifecycle
- Write basic Pod YAML files

---

# 📖 What is a Pod?

A **Pod** is the **smallest deployable unit** in Kubernetes.

A Pod wraps one or more containers and provides:

- 📦 Shared Network
- 💾 Shared Storage
- 🔗 Shared Lifecycle
- 🌐 Unique IP Address

A Pod usually contains **one container**, but it can also run multiple tightly coupled containers.

---

# 💡 Why Pods?

Instead of managing containers individually, Kubernetes manages Pods.

Without Pods:

```text
Application

↓

Individual Containers

↓

Difficult Management ❌
```

With Pods:

```text
Application

↓

Pod

↓

Container(s)

↓

Easy Management ✅
```

Benefits:

- ✅ Easy deployment
- ✅ Shared networking
- ✅ Resource sharing
- ✅ Simplified management

---

# 🏗️ Pod Architecture

```text
             Pod
     ┌──────────────────┐
     │                  │
     │  Container        │
     │                  │
     ├──────────────────┤
     │ Shared Storage   │
     ├──────────────────┤
     │ Shared Network   │
     └──────────────────┘
```

Each Pod gets:

- One IP Address
- Shared Network Namespace
- Shared Storage Volumes

---

# 📦 Single vs Multi-Container Pods

## Single Container Pod

```text
Pod

↓

Application Container
```

Most common deployment model.

---

## Multi-Container Pod

```text
Pod

├── Main Application

└── Sidecar Container
```

Examples:

- Log Collector
- Monitoring Agent
- Proxy

Containers share:

- Network
- Volumes
- Lifecycle

---

# 🔄 Pod Lifecycle

A Pod moves through several phases.

```text
Pending

↓

Running

↓

Succeeded

↓

Failed
```

Common Pod States:

| Phase | Description |
|--------|-------------|
| Pending | Pod is being created |
| Running | Pod is running |
| Succeeded | Completed successfully |
| Failed | Pod terminated with error |
| Unknown | Status cannot be determined |

---

# 🚀 Creating Pods

Create a Pod from a YAML file:

```bash
kubectl apply -f pod.yaml
```

List Pods:

```bash
kubectl get pods
```

Delete a Pod:

```bash
kubectl delete pod my-pod
```

---

# 📝 Pod YAML Example

```yaml
apiVersion: v1
kind: Pod

metadata:
  name: nginx-pod

spec:
  containers:
    - name: nginx
      image: nginx:latest
      ports:
        - containerPort: 80
```

Apply the configuration:

```bash
kubectl apply -f pod.yaml
```

---

# 🛠️ Managing Pods

Describe a Pod:

```bash
kubectl describe pod nginx-pod
```

View logs:

```bash
kubectl logs nginx-pod
```

Execute a shell:

```bash
kubectl exec -it nginx-pod -- /bin/bash
```

Delete the Pod:

```bash
kubectl delete pod nginx-pod
```

---

# 💻 Useful Pod Commands

List Pods:

```bash
kubectl get pods
```

List Pods with more details:

```bash
kubectl get pods -o wide
```

Watch Pod status:

```bash
kubectl get pods -w
```

Describe a Pod:

```bash
kubectl describe pod nginx-pod
```

View Pod logs:

```bash
kubectl logs nginx-pod
```

Delete a Pod:

```bash
kubectl delete pod nginx-pod
```

---

# 🏗️ Pod Workflow

```text
Write YAML

↓

kubectl apply

↓

API Server

↓

Scheduler

↓

Worker Node

↓

Pod Created

↓

Container Running
```

---

# 🏆 Best Practices

- ✅ One main application per Pod
- ✅ Use Deployments instead of standalone Pods for production
- ✅ Keep Pods stateless whenever possible
- ✅ Use resource requests and limits
- ✅ Configure health probes
- ✅ Use labels for organization
- ✅ Store Pod definitions in Git

---

# 🌍 Common Use Cases

| Scenario | Pod |
|----------|-----|
| Web Server | ✅ |
| API Service | ✅ |
| Database Client | ✅ |
| Batch Job | ✅ |
| Monitoring Agent | ✅ |
| Sidecar Container | ✅ |

---

# 📝 Key Takeaways

- A Pod is the smallest deployable unit in Kubernetes.
- Pods contain one or more containers.
- Containers inside a Pod share networking and storage.
- Pods are temporary and can be recreated.
- Deployments are preferred for managing Pods in production.

---

# 📋 Summary

In this chapter, you learned:

- Pods
- Pod Architecture
- Single vs Multi-Container Pods
- Pod Lifecycle
- Pod YAML
- Managing Pods
- Useful Commands

---

# ❓ Interview Questions

## Beginner

1. What is a Pod?
2. Why are Pods used?
3. Can a Pod contain multiple containers?
4. What is the smallest deployable unit in Kubernetes?
5. How do you create a Pod?

---

## Intermediate

6. Explain Pod architecture.
7. Difference between a Pod and a Container?
8. Explain the Pod lifecycle.
9. What is a Sidecar Container?
10. How do containers communicate inside a Pod?

---

## Advanced

11. Why are Pods considered ephemeral?
12. Explain Pod networking.
13. How would you troubleshoot a Pod stuck in Pending state?
14. Why shouldn't standalone Pods be used in production?
15. Explain how the Scheduler places Pods on Worker Nodes.

---

# 🎯 Practice Exercises

## Exercise 1

Create a Pod using a YAML file.

---

## Exercise 2

Deploy an Nginx Pod.

```bash
kubectl apply -f pod.yaml
```

---

## Exercise 3

View Pod details.

```bash
kubectl describe pod nginx-pod
```

---

## Exercise 4

Check Pod logs.

```bash
kubectl logs nginx-pod
```

---

## Exercise 5

Delete the Pod.

```bash
kubectl delete pod nginx-pod
```

---

# 🧩 Mini Project

Create a Markdown file named:

```text
kubernetes-pods-guide.md
```

Include:

- Pod Overview
- Pod Architecture
- Pod Lifecycle
- Pod YAML
- Pod Commands
- Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add Kubernetes Pods guide"
```

---

# 📚 Further Reading

- Kubernetes Pods Documentation
- Pod Lifecycle
- Pod Design Patterns
- Kubernetes API Reference

---

# 📚 Navigation

| ⬅️ Previous | 🏠 Home | ➡️ Next |
|------------|---------|---------|
| [04 - kubectl Basics](04-kubectl-Basics.md) | [Kubernetes Roadmap](README.md) | [06 - ReplicaSets](06-ReplicaSets.md) |

---

# 🚀 What's Next?

In **Chapter 06 – ReplicaSets**, you'll learn:

- 📦 What is a ReplicaSet?
- 🔄 Maintaining Desired State
- 📝 ReplicaSet YAML
- 📈 Scaling Pods
- 🛠️ Managing ReplicaSets
- 📊 ReplicaSet Commands
- 🚀 Best Practices
