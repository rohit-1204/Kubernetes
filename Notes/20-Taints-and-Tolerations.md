# Kubernetes Notes
# Chapter 20 - Taints and Tolerations

> 📘 **Level:** Beginner to Intermediate
> ⏱️ **Estimated Reading Time:** 60–75 minutes
> 🛠️ **Practice Time:** 3–4 hours

---

# 📚 Table of Contents

1. What are Taints?
2. What are Tolerations?
3. Why Use Taints and Tolerations?
4. Architecture
5. Taint Effects
6. Adding Taints
7. Pod Tolerations
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

- Understand Taints and Tolerations
- Control Pod scheduling
- Prevent Pods from running on specific nodes
- Configure Pod tolerations
- Manage node scheduling efficiently

---

# 📖 What are Taints?

A **Taint** is applied to a **Node** to prevent Pods from being scheduled onto it unless the Pods explicitly allow it.

Think of a taint as a **restriction** placed on a node.

Example:

```text
Node

↓

Taint Applied

↓

Only Matching Pods Can Run
```

---

# 📖 What are Tolerations?

A **Toleration** is added to a **Pod**.

It allows the Pod to be scheduled on a node that has a matching taint.

> **Important:** A toleration allows scheduling on a tainted node, but it does **not** guarantee the Pod will be scheduled there.

---

# 💡 Why Use Taints and Tolerations?

Without Taints:

```text
Node 1

↓

Any Pod Can Run ❌
```

With Taints:

```text
Node 1

↓

Taint Applied

↓

Only Authorized Pods Run ✅
```

Benefits:

- ✅ Reserve dedicated nodes
- ✅ Isolate workloads
- ✅ Protect critical applications
- ✅ Better resource management

---

# 🏗️ Architecture

```text
          Pod

            │

      Has Toleration?

        Yes      No

         │        │

         ▼        ▼

   Tainted Node   Scheduling Denied
```

---

# ⚙️ Taint Effects

There are three taint effects.

## NoSchedule

Pods without a matching toleration **cannot** be scheduled.

```text
Node + NoSchedule

↓

Only Matching Pods
```

---

## PreferNoSchedule

Kubernetes tries to avoid scheduling Pods on the node but may still place them there if necessary.

---

## NoExecute

Pods without matching tolerations are removed from the node.

Also prevents new Pods from being scheduled.

---

# 🚀 Adding Taints

Apply a taint:

```bash
kubectl taint nodes worker1 dedicated=database:NoSchedule
```

View node information:

```bash
kubectl describe node worker1
```

Remove a taint:

```bash
kubectl taint nodes worker1 dedicated=database:NoSchedule-
```

---

# 📝 Pod with Toleration

```yaml
apiVersion: v1
kind: Pod

metadata:
  name: database-pod

spec:
  tolerations:
    - key: "dedicated"
      operator: "Equal"
      value: "database"
      effect: "NoSchedule"

  containers:
    - name: mysql
      image: mysql
```

Create the Pod:

```bash
kubectl apply -f pod.yaml
```

---

# ⚙️ Managing Taints

View Nodes:

```bash
kubectl get nodes
```

Describe Node:

```bash
kubectl describe node worker1
```

View Pod:

```bash
kubectl describe pod database-pod
```

---

# 💻 Useful Commands

Add a taint:

```bash
kubectl taint nodes worker1 dedicated=database:NoSchedule
```

Remove a taint:

```bash
kubectl taint nodes worker1 dedicated=database:NoSchedule-
```

View Nodes:

```bash
kubectl get nodes
```

Describe Node:

```bash
kubectl describe node worker1
```

Describe Pod:

```bash
kubectl describe pod database-pod
```

---

# 🏗️ Scheduling Workflow

```text
Node

↓

Taint Applied

↓

Pod Created

↓

Has Matching Toleration?

↓

Yes → Scheduled

No → Not Scheduled
```

---

# 🏆 Best Practices

- ✅ Use taints to reserve dedicated nodes.
- ✅ Keep taints simple and meaningful.
- ✅ Use tolerations only when required.
- ✅ Combine with node labels for better scheduling.
- ✅ Monitor scheduling events.
- ✅ Document node roles clearly.

---

# 🌍 Common Use Cases

| Scenario | Taints & Tolerations |
|----------|----------------------|
| Database Nodes | ✅ |
| GPU Nodes | ✅ |
| Monitoring Nodes | ✅ |
| Dedicated Production Nodes | ✅ |
| Critical Applications | ✅ |

---

# 🔄 Node Selector vs Taints

| Node Selector | Taints & Tolerations |
|---------------|----------------------|
| Attracts Pods to nodes | Repels Pods from nodes |
| Pod chooses node | Node controls scheduling |
| Simple scheduling | Advanced scheduling |
| Optional | Restrictive |

---

# 📝 Key Takeaways

- Taints restrict Pod scheduling.
- Tolerations allow Pods to run on tainted nodes.
- They help isolate workloads.
- Three effects are available: NoSchedule, PreferNoSchedule, and NoExecute.
- Commonly used in production Kubernetes clusters.

---

# 📋 Summary

In this chapter, you learned:

- Taints
- Tolerations
- Taint Effects
- YAML Example
- Commands
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is a Taint?
2. What is a Toleration?
3. Why do we use Taints?
4. What is NoSchedule?
5. How do you add a taint?

---

## Intermediate

6. Explain NoExecute.
7. Difference between Taints and Node Selectors?
8. What happens if a Pod has no matching toleration?
9. How do you remove a taint?
10. Give production use cases for Taints.

---

## Advanced

11. Explain Kubernetes scheduling with Taints and Tolerations.
12. Why are GPU nodes often tainted?
13. How would you dedicate nodes for database workloads?
14. When should PreferNoSchedule be used?
15. How do Taints improve cluster resource utilization?

---

# 🎯 Practice Exercises

## Exercise 1

Add a taint to a worker node.

---

## Exercise 2

View the taint.

```bash
kubectl describe node worker1
```

---

## Exercise 3

Create a Pod with a matching toleration.

---

## Exercise 4

Verify Pod scheduling.

```bash
kubectl get pods -o wide
```

---

## Exercise 5

Remove the taint.

```bash
kubectl taint nodes worker1 dedicated=database:NoSchedule-
```

---

# 🧩 Mini Project

Create a Markdown file named:

```text
kubernetes-taints-guide.md
```

Include:

- Taints Overview
- Tolerations
- Taint Effects
- YAML Example
- Commands
- Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add Kubernetes Taints and Tolerations guide"
```

---

# 📚 Further Reading

- Kubernetes Taints and Tolerations Documentation
- Kubernetes Scheduling
- Kubernetes Node Management
- Kubernetes API Reference

---

# 📚 Navigation

| ⬅️ Previous | 🏠 Home | ➡️ Next |
|------------|---------|---------|
| [19 - Jobs and CronJobs](19-Jobs-and-CronJobs.md) | [Kubernetes Roadmap](README.md) | [21 - Node Affinity.md](21-Node-Affinity.md) |

---

# 🚀 What's Next?

In **Chapter 21 – Node Affinity**, you'll learn:

- 🖥️ What is Node Affinity?
- 🏷️ Node Labels
- 📍 Required vs Preferred Affinity
- 📝 Affinity YAML
- 💻 Affinity Commands
- 🛠️ Best Practices
