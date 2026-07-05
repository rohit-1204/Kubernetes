# Kubernetes Notes
# Chapter 21 - Node Selectors and Affinity

> 📘 **Level:** Beginner to Intermediate
> ⏱️ **Estimated Reading Time:** 60–75 minutes
> 🛠️ **Practice Time:** 3–4 hours

---

# 📚 Table of Contents

1. What are Node Selectors?
2. What is Node Affinity?
3. Why Use Node Scheduling?
4. Architecture
5. Node Labels
6. Node Selector YAML
7. Node Affinity YAML
8. Types of Node Affinity
9. Useful Commands
10. Best Practices
11. Summary
12. Interview Questions
13. Practice Exercises
14. Mini Project
15. Further Reading

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Understand Node Selectors
- Learn Node Affinity
- Schedule Pods on specific Nodes
- Use Node Labels
- Configure advanced scheduling policies

---

# 📖 What are Node Selectors?

A **Node Selector** is the simplest way to schedule a Pod on a specific Node.

It works by matching **Node Labels** with the Pod's `nodeSelector`.

Example:

```text
Node Label

disk=ssd

↓

Pod

nodeSelector:
disk=ssd

↓

Pod Scheduled
```

---

# 📖 What is Node Affinity?

**Node Affinity** is an advanced version of Node Selector.

It allows flexible scheduling rules using expressions and conditions.

Benefits:

- More powerful than Node Selectors
- Supports multiple conditions
- Preferred and required scheduling

---

# 💡 Why Use Node Scheduling?

Without Scheduling Rules:

```text
Cluster

↓

Pods

↓

Random Node Placement ❌
```

With Node Selectors & Affinity:

```text
Cluster

↓

Labels

↓

Matching Node

↓

Correct Placement ✅
```

Benefits:

- ✅ Better resource utilization
- ✅ Dedicated workloads
- ✅ Improved performance
- ✅ Easier workload management

---

# 🏗️ Architecture

```text
           Pod

            │

     Scheduling Rule

            │

      Label Matching

            │

            ▼

      Matching Node
```

---

# 🏷️ Node Labels

Add a label:

```bash
kubectl label nodes worker1 disk=ssd
```

View labels:

```bash
kubectl get nodes --show-labels
```

Remove a label:

```bash
kubectl label nodes worker1 disk-
```

---

# 📝 Node Selector YAML

```yaml
apiVersion: v1
kind: Pod

metadata:
  name: nginx-pod

spec:
  nodeSelector:
    disk: ssd

  containers:
    - name: nginx
      image: nginx
```

Create the Pod:

```bash
kubectl apply -f pod.yaml
```

---

# 📝 Node Affinity YAML

```yaml
apiVersion: v1
kind: Pod

metadata:
  name: nginx-pod

spec:
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
          - matchExpressions:
              - key: disk
                operator: In
                values:
                  - ssd

  containers:
    - name: nginx
      image: nginx
```

Create the Pod:

```bash
kubectl apply -f affinity.yaml
```

---

# 🔄 Types of Node Affinity

## Required Affinity

The Pod **must** be scheduled on a node that matches the rule.

```text
Rule Matches

↓

Pod Scheduled
```

If no node matches, the Pod remains **Pending**.

---

## Preferred Affinity

Kubernetes tries to schedule the Pod on a matching node.

If no matching node is available, the Pod can still run on another node.

---

# 💻 Useful Commands

Add Label:

```bash
kubectl label nodes worker1 disk=ssd
```

View Labels:

```bash
kubectl get nodes --show-labels
```

Describe Node:

```bash
kubectl describe node worker1
```

View Pods:

```bash
kubectl get pods -o wide
```

Remove Label:

```bash
kubectl label nodes worker1 disk-
```

---

# 🏗️ Scheduling Workflow

```text
Node Label

↓

Pod Created

↓

Node Selector / Affinity

↓

Matching Node

↓

Pod Scheduled
```

---

# 🏆 Best Practices

- ✅ Use labels with meaningful names.
- ✅ Prefer Node Affinity for complex scheduling.
- ✅ Use Required Affinity only when necessary.
- ✅ Keep labels consistent across nodes.
- ✅ Document node labels.
- ✅ Monitor scheduling events.

---

# 🌍 Common Use Cases

| Scenario | Node Selector | Node Affinity |
|----------|---------------|---------------|
| SSD Storage Nodes | ✅ | ✅ |
| GPU Nodes | ✅ | ✅ |
| Database Servers | ✅ | ✅ |
| High Memory Nodes | ✅ | ✅ |
| Production Nodes | ✅ | ✅ |

---

# 🔄 Node Selector vs Node Affinity

| Node Selector | Node Affinity |
|---------------|---------------|
| Simple matching | Advanced matching |
| Exact label match | Expressions & operators |
| Basic scheduling | Flexible scheduling |
| Easy to configure | More powerful |

---

# 📝 Key Takeaways

- Node Selectors schedule Pods using labels.
- Node Affinity provides advanced scheduling rules.
- Labels identify node characteristics.
- Required Affinity is mandatory.
- Preferred Affinity is a scheduling preference.

---

# 📋 Summary

In this chapter, you learned:

- Node Selectors
- Node Labels
- Node Affinity
- Required & Preferred Affinity
- YAML Examples
- Commands
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is a Node Selector?
2. What is Node Affinity?
3. Why do Nodes use labels?
4. How do you add a node label?
5. How do you list node labels?

---

## Intermediate

6. Difference between Node Selector and Node Affinity?
7. Explain Required Affinity.
8. Explain Preferred Affinity.
9. What happens if no matching node exists?
10. How do you remove a node label?

---

## Advanced

11. Explain Kubernetes scheduling using Node Affinity.
12. Why is Node Affinity preferred over Node Selectors?
13. How would you dedicate SSD nodes for databases?
14. Explain matchExpressions.
15. Compare Node Affinity with Taints and Tolerations.

---

# 🎯 Practice Exercises

## Exercise 1

Add a label to a worker node.

```bash
kubectl label nodes worker1 disk=ssd
```

---

## Exercise 2

Verify node labels.

```bash
kubectl get nodes --show-labels
```

---

## Exercise 3

Create a Pod using a Node Selector.

---

## Exercise 4

Create a Pod using Node Affinity.

---

## Exercise 5

Remove the label.

```bash
kubectl label nodes worker1 disk-
```

---

# 🧩 Mini Project

Create a Markdown file named:

```text
kubernetes-node-affinity-guide.md
```

Include:

- Node Selectors
- Node Labels
- Node Affinity
- YAML Examples
- Commands
- Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add Kubernetes Node Affinity guide"
```

---

# 📚 Further Reading

- Kubernetes Node Affinity Documentation
- Kubernetes Scheduling
- Kubernetes Labels Documentation
- Kubernetes API Reference

---

# 📚 Navigation

| ⬅️ Previous | 🏠 Home | ➡️ Next |
|------------|---------|---------|
| [20 - Taints and Tolerations](20-Taints-and-Tolerations.md) | [Kubernetes Roadmap](README.md) | [22 - Helm.md](22-Helm.md) |

---

# 🚀 What's Next?

In **Chapter 22 – Helm**, you'll learn:

- ⛵ What is Helm?
- 📦 Helm Charts
- 🚀 Installing Helm
- 🔄 Helm Releases
- 💻 Helm Commands
- 📁 Chart Structure
- 🛠️ Best Practices
