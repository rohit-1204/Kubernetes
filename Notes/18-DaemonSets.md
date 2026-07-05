# Kubernetes Notes
# Chapter 18 - DaemonSets

> 📘 **Level:** Beginner to Intermediate
> ⏱️ **Estimated Reading Time:** 50–60 minutes
> 🛠️ **Practice Time:** 2–3 hours

---

# 📚 Table of Contents

1. What is a DaemonSet?
2. Why Use DaemonSets?
3. DaemonSet Architecture
4. How DaemonSets Work
5. DaemonSet YAML
6. Common Use Cases
7. Managing DaemonSets
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

- Understand Kubernetes DaemonSets
- Learn how DaemonSets schedule Pods
- Deploy one Pod on every worker node
- Manage DaemonSets using kubectl
- Understand common production use cases

---

# 📖 What is a DaemonSet?

A **DaemonSet** is a Kubernetes workload that ensures **one Pod runs on every worker node** in the cluster.

Whenever a new node joins the cluster, Kubernetes automatically creates a DaemonSet Pod on that node.

If a node is removed, the corresponding Pod is also removed.

---

# 💡 Why Use DaemonSets?

Without DaemonSet:

```text
Node 1   → Logging Agent

Node 2   → No Logging Agent

Node 3   → No Logging Agent

Inconsistent Deployment ❌
```

With DaemonSet:

```text
Node 1   → Logging Agent

Node 2   → Logging Agent

Node 3   → Logging Agent

Every Node Covered ✅
```

Benefits:

- ✅ Automatic deployment on every node
- ✅ Easy node monitoring
- ✅ Centralized logging
- ✅ Consistent cluster configuration

---

# 🏗️ DaemonSet Architecture

```text
           DaemonSet
                │
      ┌─────────┼─────────┐
      ▼         ▼         ▼
   Worker 1  Worker 2  Worker 3
      │         │         │
      ▼         ▼         ▼
    Pod       Pod       Pod
```

Each worker node runs exactly one DaemonSet Pod.

---

# ⚙️ How DaemonSets Work

1. Create a DaemonSet.
2. Kubernetes schedules one Pod on each worker node.
3. New nodes automatically receive a Pod.
4. Deleted nodes remove their Pod automatically.

This ensures cluster-wide services are always available.

---

# 📝 DaemonSet YAML

```yaml
apiVersion: apps/v1
kind: DaemonSet

metadata:
  name: fluentd

spec:
  selector:
    matchLabels:
      app: fluentd

  template:
    metadata:
      labels:
        app: fluentd

    spec:
      containers:
        - name: fluentd
          image: fluent/fluentd
```

Create the DaemonSet:

```bash
kubectl apply -f daemonset.yaml
```

---

# 🌍 Common Use Cases

DaemonSets are commonly used for:

- Log collection (Fluentd, Fluent Bit)
- Monitoring agents (Prometheus Node Exporter)
- Security agents
- Networking plugins (CNI)
- Storage plugins (CSI)

---

# ⚙️ Managing DaemonSets

List DaemonSets:

```bash
kubectl get daemonsets
```

Describe a DaemonSet:

```bash
kubectl describe daemonset fluentd
```

Delete a DaemonSet:

```bash
kubectl delete daemonset fluentd
```

---

# 💻 Useful Commands

Create DaemonSet:

```bash
kubectl apply -f daemonset.yaml
```

List DaemonSets:

```bash
kubectl get ds
```

Describe DaemonSet:

```bash
kubectl describe ds fluentd
```

View Pods:

```bash
kubectl get pods -o wide
```

Delete DaemonSet:

```bash
kubectl delete ds fluentd
```

---

# 🏗️ DaemonSet Workflow

```text
Create DaemonSet

↓

One Pod Per Node

↓

New Node Added

↓

Pod Automatically Created

↓

Cluster Remains Consistent
```

---

# 🏆 Best Practices

- ✅ Use DaemonSets for node-level applications.
- ✅ Keep DaemonSet containers lightweight.
- ✅ Monitor DaemonSet health regularly.
- ✅ Use labels for easy management.
- ✅ Store DaemonSet YAML in Git.
- ✅ Update DaemonSets using rolling updates.

---

# 🌍 Common Use Cases

| Scenario | DaemonSet |
|----------|-----------|
| Log Collection | ✅ |
| Monitoring Agents | ✅ |
| Network Plugins | ✅ |
| Security Agents | ✅ |
| Storage Plugins | ✅ |

---

# 🔄 DaemonSet vs Deployment

| Deployment | DaemonSet |
|------------|-----------|
| Runs specified number of Pods | Runs one Pod per node |
| Used for applications | Used for node services |
| Supports scaling | Automatically scales with nodes |
| User defines replicas | Kubernetes manages Pods per node |

---

# 📝 Key Takeaways

- DaemonSets run one Pod on every worker node.
- New nodes automatically receive DaemonSet Pods.
- Commonly used for logging, monitoring, and networking.
- DaemonSets simplify cluster-wide service deployment.
- They are essential for many production Kubernetes clusters.

---

# 📋 Summary

In this chapter, you learned:

- DaemonSets
- DaemonSet Architecture
- YAML Example
- Commands
- Use Cases
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is a DaemonSet?
2. Why do we use DaemonSets?
3. How many Pods does a DaemonSet run on a node?
4. How do you list DaemonSets?
5. Give two use cases for DaemonSets.

---

## Intermediate

6. Explain DaemonSet architecture.
7. Difference between Deployment and DaemonSet?
8. What happens when a new node joins the cluster?
9. How do you update a DaemonSet?
10. Why are monitoring agents deployed as DaemonSets?

---

## Advanced

11. Explain how DaemonSets are scheduled.
12. How do DaemonSets support cluster operations?
13. When should you use a Deployment instead of a DaemonSet?
14. Why are CNI plugins commonly deployed as DaemonSets?
15. How would you deploy a logging solution across all nodes?

---

# 🎯 Practice Exercises

## Exercise 1

Create a DaemonSet.

---

## Exercise 2

List all DaemonSets.

```bash
kubectl get ds
```

---

## Exercise 3

Verify one Pod is running on each node.

```bash
kubectl get pods -o wide
```

---

## Exercise 4

Describe the DaemonSet.

```bash
kubectl describe ds fluentd
```

---

## Exercise 5

Delete the DaemonSet.

```bash
kubectl delete ds fluentd
```

---

# 🧩 Mini Project

Create a Markdown file named:

```text
kubernetes-daemonsets-guide.md
```

Include:

- DaemonSet Overview
- Architecture
- YAML Example
- Commands
- Common Use Cases
- Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add Kubernetes DaemonSets guide"
```

---

# 📚 Further Reading

- Kubernetes DaemonSet Documentation
- Kubernetes Workloads
- Kubernetes Scheduling
- Kubernetes API Reference

---

# 📚 Navigation

| ⬅️ Previous | 🏠 Home | ➡️ Next |
|------------|---------|---------|
| [17 - StorageClasses](17-StorageClasses.md) | [Kubernetes Roadmap](README.md) | [19 - Jobs-and-CronJobs.md](19-Jobs-and-CronJobs.md) |

---

# 🚀 What's Next?

In **Chapter 19 – Jobs and CronJobs**, you'll learn:

- ⚡ What are Jobs?
- ⏰ What are CronJobs?
- 📝 Job YAML
- 🗓️ Scheduling Jobs
- 🔄 Retry Policies
- 💻 Job Commands
- 🛠️ Best Practices
