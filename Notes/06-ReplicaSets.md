# Kubernetes Notes
# Chapter 06 - ReplicaSets

> 📘 **Level:** Beginner
> ⏱️ **Estimated Reading Time:** 60–75 minutes
> 🛠️ **Practice Time:** 3–4 hours

---

# 📚 Table of Contents

1. What is a ReplicaSet?
2. Why Use ReplicaSets?
3. How ReplicaSets Work
4. ReplicaSet Architecture
5. ReplicaSet YAML
6. Scaling ReplicaSets
7. Managing ReplicaSets
8. Useful Commands
9. Best Practices
10. Summary
11. Interview Questions
12. Practice Exercises
13. Mini Project
14. Further Reading

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Understand ReplicaSets
- Maintain multiple Pod replicas
- Scale applications
- Create ReplicaSets using YAML
- Manage ReplicaSets using kubectl

---

# 📖 What is a ReplicaSet?

A **ReplicaSet** is a Kubernetes resource that ensures a specified number of identical **Pods** are always running.

If a Pod fails or is deleted, the ReplicaSet automatically creates a new Pod to maintain the desired number of replicas.

---

# 💡 Why Use ReplicaSets?

Without a ReplicaSet:

```text
3 Pods Running

↓

1 Pod Crashes

↓

Only 2 Pods Running ❌
```

With a ReplicaSet:

```text
3 Pods Running

↓

1 Pod Crashes

↓

ReplicaSet Creates New Pod

↓

3 Pods Running ✅
```

Benefits:

- ✅ High Availability
- ✅ Automatic Recovery
- ✅ Easy Scaling
- ✅ Desired State Management

---

# ⚙️ How ReplicaSets Work

ReplicaSets continuously monitor Pods.

Workflow:

```text
Desired Replicas = 3

↓

Current Pods = 2

↓

ReplicaSet Detects Difference

↓

Creates New Pod

↓

Current Pods = 3
```

---

# 🏗️ ReplicaSet Architecture

```text
          ReplicaSet
               │
      Desired Replicas = 3
               │
      ┌────────┼────────┐
      ▼        ▼        ▼
    Pod 1    Pod 2    Pod 3
```

If any Pod is removed, ReplicaSet automatically recreates it.

---

# 📝 ReplicaSet YAML

```yaml
apiVersion: apps/v1
kind: ReplicaSet

metadata:
  name: nginx-rs

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
```

Create the ReplicaSet:

```bash
kubectl apply -f replicaset.yaml
```

---

# 📈 Scaling ReplicaSets

Scale using kubectl:

```bash
kubectl scale replicaset nginx-rs --replicas=5
```

Verify:

```bash
kubectl get rs
```

Kubernetes automatically creates or removes Pods to match the desired replica count.

---

# 🛠️ Managing ReplicaSets

List ReplicaSets:

```bash
kubectl get rs
```

Describe a ReplicaSet:

```bash
kubectl describe rs nginx-rs
```

View Pods:

```bash
kubectl get pods
```

Delete a ReplicaSet:

```bash
kubectl delete rs nginx-rs
```

---

# 💻 Useful Commands

Create ReplicaSet:

```bash
kubectl apply -f replicaset.yaml
```

List ReplicaSets:

```bash
kubectl get rs
```

Describe ReplicaSet:

```bash
kubectl describe rs nginx-rs
```

Scale ReplicaSet:

```bash
kubectl scale rs nginx-rs --replicas=5
```

Delete ReplicaSet:

```bash
kubectl delete rs nginx-rs
```

---

# 🏗️ ReplicaSet Workflow

```text
Create ReplicaSet

↓

Desired Replicas = 3

↓

Pods Created

↓

Pod Fails

↓

ReplicaSet Detects Failure

↓

New Pod Created

↓

Desired State Restored
```

---

# 🏆 Best Practices

- ✅ Use Deployments instead of standalone ReplicaSets for production.
- ✅ Use labels and selectors consistently.
- ✅ Monitor Pod health.
- ✅ Define resource requests and limits.
- ✅ Store YAML files in version control.
- ✅ Scale applications based on workload.

---

# 🌍 Common Use Cases

| Scenario | ReplicaSet |
|----------|------------|
| Web Application | ✅ |
| API Service | ✅ |
| High Availability | ✅ |
| Pod Recovery | ✅ |
| Horizontal Scaling | ✅ |

---

# 🔄 ReplicaSet vs Pod

| Pod | ReplicaSet |
|-----|------------|
| Runs a single application instance | Manages multiple Pod replicas |
| No automatic recovery | Automatically recreates failed Pods |
| Manual scaling | Automatic and manual scaling |
| Best for testing | Best for production workloads |

---

# 📝 Key Takeaways

- ReplicaSets ensure the desired number of Pods are always running.
- Failed Pods are recreated automatically.
- ReplicaSets provide high availability.
- Scaling is achieved by changing the replica count.
- Deployments internally use ReplicaSets.

---

# 📋 Summary

In this chapter, you learned:

- ReplicaSets
- Desired State
- ReplicaSet Architecture
- ReplicaSet YAML
- Scaling
- Management Commands
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is a ReplicaSet?
2. Why do we use ReplicaSets?
3. What happens if a Pod fails?
4. How do you scale a ReplicaSet?
5. Which command lists ReplicaSets?

---

## Intermediate

6. Explain how ReplicaSets maintain desired state.
7. What is the purpose of labels and selectors?
8. Difference between a Pod and a ReplicaSet?
9. How do ReplicaSets improve availability?
10. How do you delete a ReplicaSet?

---

## Advanced

11. Explain the ReplicaSet lifecycle.
12. Why are Deployments preferred over ReplicaSets?
13. How does Kubernetes detect failed Pods?
14. Explain ReplicaSet reconciliation.
15. How would you troubleshoot a ReplicaSet not creating Pods?

---

# 🎯 Practice Exercises

## Exercise 1

Create a ReplicaSet using YAML.

---

## Exercise 2

Deploy three Nginx Pods.

```bash
kubectl apply -f replicaset.yaml
```

---

## Exercise 3

Scale the ReplicaSet to five replicas.

```bash
kubectl scale rs nginx-rs --replicas=5
```

---

## Exercise 4

Delete one Pod and observe automatic recreation.

```bash
kubectl delete pod <pod-name>
```

---

## Exercise 5

Delete the ReplicaSet.

```bash
kubectl delete rs nginx-rs
```

---

# 🧩 Mini Project

Create a Markdown file named:

```text
kubernetes-replicaset-guide.md
```

Include:

- ReplicaSet Overview
- Architecture
- YAML Example
- Scaling
- Commands
- Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add Kubernetes ReplicaSet guide"
```

---

# 📚 Further Reading

- Kubernetes ReplicaSet Documentation
- Kubernetes Workloads
- Labels and Selectors
- Kubernetes API Reference

---

# 📚 Navigation

| ⬅️ Previous | 🏠 Home | ➡️ Next |
|------------|---------|---------|
| [05 - Pods](05-Pods.md) | [Kubernetes Roadmap](README.md) | [07 - Deployments](07-Deployments.md) |

---

# 🚀 What's Next?

In **Chapter 07 – Deployments**, you'll learn:

- 🚀 What is a Deployment?
- 📦 Deployment Architecture
- 📝 Deployment YAML
- 📈 Scaling Applications
- 🔄 Rolling Updates
- ⏪ Rollbacks
- 🛠️ Deployment Best Practices
