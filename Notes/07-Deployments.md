# Kubernetes Notes
# Chapter 07 - Deployments

> 📘 **Level:** Beginner
> ⏱️ **Estimated Reading Time:** 60–75 minutes
> 🛠️ **Practice Time:** 3–4 hours

---

# 📚 Table of Contents

1. What is a Deployment?
2. Why Use Deployments?
3. Deployment Architecture
4. Deployment YAML
5. Creating Deployments
6. Scaling Deployments
7. Rolling Updates
8. Rollbacks
9. Managing Deployments
10. Useful Commands
11. Best Practices
12. Summary
13. Interview Questions
14. Practice Exercises
15. Mini Project
16. Further Reading

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Understand Kubernetes Deployments
- Create and manage Deployments
- Scale applications
- Perform rolling updates
- Roll back failed deployments

---

# 📖 What is a Deployment?

A **Deployment** is a Kubernetes resource that manages the lifecycle of Pods and ReplicaSets.

It provides:

- 🚀 Automated Deployments
- 📈 Scaling
- 🔄 Rolling Updates
- ⏪ Rollbacks
- ❤️ Self-Healing

Deployments are the **recommended way** to run applications in Kubernetes.

---

# 💡 Why Use Deployments?

Without Deployments:

```text
Create Pods

↓

Manage Manually

↓

High Maintenance ❌
```

With Deployments:

```text
Deployment

↓

ReplicaSet

↓

Pods

↓

Automatic Management ✅
```

Benefits:

- ✅ Easy scaling
- ✅ Automatic recovery
- ✅ Version control
- ✅ Zero-downtime updates

---

# 🏗️ Deployment Architecture

```text
          Deployment
                │
                ▼
          ReplicaSet
                │
      ┌─────────┼─────────┐
      ▼         ▼         ▼
    Pod 1     Pod 2     Pod 3
```

Deployment manages ReplicaSets, and ReplicaSets manage Pods.

---

# 📝 Deployment YAML

```yaml
apiVersion: apps/v1
kind: Deployment

metadata:
  name: nginx-deployment

spec:
  replicas: 3

  selector:
    matchLabels:
      app: nginx

  template:
    metadata:
      labels:
        app: nginx

    spec:
      containers:
        - name: nginx
          image: nginx:latest
          ports:
            - containerPort: 80
```

Create the Deployment:

```bash
kubectl apply -f deployment.yaml
```

---

# 🚀 Creating Deployments

Apply a Deployment:

```bash
kubectl apply -f deployment.yaml
```

List Deployments:

```bash
kubectl get deployments
```

View Pods:

```bash
kubectl get pods
```

---

# 📈 Scaling Deployments

Increase replicas:

```bash
kubectl scale deployment nginx-deployment --replicas=5
```

Check status:

```bash
kubectl get deployment
```

Kubernetes automatically creates or removes Pods.

---

# 🔄 Rolling Updates

Rolling Updates allow you to update applications **without downtime**.

Update image:

```bash
kubectl set image deployment/nginx-deployment \
nginx=nginx:1.25
```

Monitor rollout:

```bash
kubectl rollout status deployment/nginx-deployment
```

Workflow:

```text
Old Pods

↓

New Pods Created

↓

Old Pods Removed

↓

Deployment Updated
```

---

# ⏪ Rollbacks

If an update fails, Kubernetes can roll back to the previous version.

View rollout history:

```bash
kubectl rollout history deployment nginx-deployment
```

Rollback:

```bash
kubectl rollout undo deployment nginx-deployment
```

---

# 🛠️ Managing Deployments

Describe Deployment:

```bash
kubectl describe deployment nginx-deployment
```

Delete Deployment:

```bash
kubectl delete deployment nginx-deployment
```

Restart Deployment:

```bash
kubectl rollout restart deployment nginx-deployment
```

Pause Deployment:

```bash
kubectl rollout pause deployment nginx-deployment
```

Resume Deployment:

```bash
kubectl rollout resume deployment nginx-deployment
```

---

# 💻 Useful Commands

Create Deployment:

```bash
kubectl apply -f deployment.yaml
```

List Deployments:

```bash
kubectl get deployments
```

Describe Deployment:

```bash
kubectl describe deployment nginx-deployment
```

Scale Deployment:

```bash
kubectl scale deployment nginx-deployment --replicas=5
```

Restart Deployment:

```bash
kubectl rollout restart deployment nginx-deployment
```

Rollback Deployment:

```bash
kubectl rollout undo deployment nginx-deployment
```

Delete Deployment:

```bash
kubectl delete deployment nginx-deployment
```

---

# 🏗️ Deployment Workflow

```text
Create Deployment

↓

Deployment

↓

ReplicaSet

↓

Pods Running

↓

Update Application

↓

Rolling Update

↓

New Version Running
```

---

# 🏆 Best Practices

- ✅ Use Deployments for stateless applications
- ✅ Use Rolling Updates
- ✅ Keep replica count greater than one
- ✅ Monitor rollout status
- ✅ Use versioned container images
- ✅ Store Deployment YAML in Git
- ✅ Configure readiness and liveness probes

---

# 🌍 Common Use Cases

| Scenario | Deployment |
|----------|------------|
| Web Applications | ✅ |
| REST APIs | ✅ |
| Microservices | ✅ |
| Stateless Services | ✅ |
| Production Workloads | ✅ |

---

# 🔄 Deployment vs ReplicaSet

| Deployment | ReplicaSet |
|------------|------------|
| Manages ReplicaSets | Manages Pods |
| Supports Rolling Updates | No Rolling Updates |
| Supports Rollbacks | No Rollbacks |
| Recommended for Production | Mostly managed by Deployments |

---

# 📝 Key Takeaways

- Deployments are the recommended way to manage applications.
- They create and manage ReplicaSets.
- Rolling Updates minimize downtime.
- Rollbacks restore previous versions.
- Deployments simplify application lifecycle management.

---

# 📋 Summary

In this chapter, you learned:

- Deployments
- Deployment Architecture
- Deployment YAML
- Scaling
- Rolling Updates
- Rollbacks
- Management Commands

---

# ❓ Interview Questions

## Beginner

1. What is a Deployment?
2. Why are Deployments used?
3. How do you create a Deployment?
4. How do you scale a Deployment?
5. Which command lists Deployments?

---

## Intermediate

6. Explain Deployment architecture.
7. What is a Rolling Update?
8. How do Rollbacks work?
9. Difference between Deployment and ReplicaSet?
10. How do you restart a Deployment?

---

## Advanced

11. Explain the Deployment lifecycle.
12. How does Kubernetes achieve zero-downtime deployments?
13. How would you troubleshoot a failed rollout?
14. Why should Deployments use versioned images instead of `latest`?
15. How do Deployments ensure application availability?

---

# 🎯 Practice Exercises

## Exercise 1

Create a Deployment using YAML.

---

## Exercise 2

Deploy an Nginx application.

```bash
kubectl apply -f deployment.yaml
```

---

## Exercise 3

Scale the Deployment to five replicas.

```bash
kubectl scale deployment nginx-deployment --replicas=5
```

---

## Exercise 4

Update the container image.

```bash
kubectl set image deployment/nginx-deployment nginx=nginx:1.25
```

---

## Exercise 5

Rollback the Deployment.

```bash
kubectl rollout undo deployment nginx-deployment
```

---

# 🧩 Mini Project

Create a Markdown file named:

```text
kubernetes-deployment-guide.md
```

Include:

- Deployment Overview
- Architecture
- YAML Example
- Scaling
- Rolling Updates
- Rollbacks
- Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add Kubernetes Deployment guide"
```

---

# 📚 Further Reading

- Kubernetes Deployment Documentation
- Kubernetes Workloads
- Rolling Updates
- Kubernetes API Reference

---

# 📚 Navigation

| ⬅️ Previous | 🏠 Home | ➡️ Next |
|------------|---------|---------|
| [06 - ReplicaSets](06-ReplicaSets.md) | [Kubernetes Roadmap](README.md) | [08 - Namespaces](08-Namespaces.md) |

---

# 🚀 What's Next?

In **Chapter 08 – Namespaces**, you'll learn:

- 📂 What are Namespaces?
- 🏗️ Namespace Architecture
- 📝 Creating Namespaces
- 🔍 Managing Resources
- 🔐 Namespace Isolation
- 💻 Namespace Commands
- 🛠️ Best Practices
