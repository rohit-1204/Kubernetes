# Kubernetes Notes
# Chapter 08 - Namespaces

> 📘 **Level:** Beginner
> ⏱️ **Estimated Reading Time:** 45–60 minutes
> 🛠️ **Practice Time:** 2–3 hours

---

# 📚 Table of Contents

1. What are Namespaces?
2. Why Use Namespaces?
3. Default Namespaces
4. Namespace Architecture
5. Creating Namespaces
6. Managing Namespaces
7. Resource Isolation
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

- Understand Kubernetes Namespaces
- Create and manage Namespaces
- Isolate workloads
- Organize cluster resources
- Use namespace-specific kubectl commands

---

# 📖 What are Namespaces?

A **Namespace** is a logical partition inside a Kubernetes cluster that helps organize and isolate resources.

Namespaces allow multiple teams or applications to share the same cluster without interfering with each other.

---

# 💡 Why Use Namespaces?

Without Namespaces:

```text
Cluster

↓

All Resources Together

↓

Difficult to Manage ❌
```

With Namespaces:

```text
Cluster

├── Development

├── Testing

└── Production

↓

Easy Organization ✅
```

Benefits:

- ✅ Resource isolation
- ✅ Better organization
- ✅ Team separation
- ✅ Access control
- ✅ Resource quotas

---

# 📂 Default Namespaces

Kubernetes provides several built-in namespaces.

| Namespace | Purpose |
|-----------|---------|
| default | Default namespace for resources |
| kube-system | Kubernetes system components |
| kube-public | Publicly accessible resources |
| kube-node-lease | Node heartbeat information |

---

# 🏗️ Namespace Architecture

```text
               Kubernetes Cluster
                      │
        ┌─────────────┼─────────────┐
        ▼             ▼             ▼
   Development      Testing     Production
        │             │             │
      Pods         Services      Deployments
```

Each namespace has its own resources.

---

# 🚀 Creating Namespaces

Create a namespace:

```bash
kubectl create namespace dev
```

List namespaces:

```bash
kubectl get namespaces
```

Delete a namespace:

```bash
kubectl delete namespace dev
```

---

# 📝 Namespace YAML

```yaml
apiVersion: v1
kind: Namespace

metadata:
  name: development
```

Apply the configuration:

```bash
kubectl apply -f namespace.yaml
```

---

# 🔒 Resource Isolation

Resources inside one namespace are isolated from others.

Example:

```text
Development

↓

Frontend Pods

-----------------------

Production

↓

Frontend Pods
```

Both namespaces can have resources with the same name.

---

# ⚙️ Working with Namespaces

Create a Pod inside a namespace:

```bash
kubectl apply -f pod.yaml -n development
```

List Pods in a namespace:

```bash
kubectl get pods -n development
```

Describe a namespace:

```bash
kubectl describe namespace development
```
Switch a namespace:

```bash
kubectl config set-context --current --namespace=dev
```

Check Current namespace:

```bash
kubectl config view --minify | findstr namespace
```
---

# 💻 Useful Commands

List namespaces:

```bash
kubectl get ns
```

Switch namespace temporarily:

```bash
kubectl get pods -n development
```

Delete namespace:

```bash
kubectl delete ns development
```

View all resources in a namespace:

```bash
kubectl get all -n development
```

---

# 🏗️ Namespace Workflow

```text
Create Namespace

↓

Deploy Resources

↓

Manage Resources

↓

Isolate Workloads

↓

Delete Namespace (Optional)
```

---

# 🏆 Best Practices

- ✅ Create separate namespaces for Dev, Test, and Production.
- ✅ Use meaningful namespace names.
- ✅ Apply Resource Quotas for shared clusters.
- ✅ Use Role-Based Access Control (RBAC).
- ✅ Avoid deploying everything in the default namespace.
- ✅ Store namespace manifests in Git.

---

# 🌍 Common Use Cases

| Scenario | Namespace |
|----------|-----------|
| Development | ✅ |
| Testing | ✅ |
| Production | ✅ |
| Team Isolation | ✅ |
| Multi-Tenant Clusters | ✅ |

---

# 🔄 Namespace vs Cluster

| Namespace | Cluster |
|-----------|---------|
| Logical isolation | Physical/virtual Kubernetes environment |
| Organizes resources | Contains all namespaces |
| Shares cluster resources | Hosts all workloads |

---

# 📝 Key Takeaways

- Namespaces logically separate Kubernetes resources.
- They improve organization and security.
- Multiple applications can share one cluster safely.
- Namespaces support resource isolation and access control.
- Production clusters commonly use multiple namespaces.

---

# 📋 Summary

In this chapter, you learned:

- Namespaces
- Default Namespaces
- Namespace YAML
- Resource Isolation
- Namespace Commands
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is a Namespace?
2. Why are Namespaces used?
3. What is the default namespace?
4. How do you create a Namespace?
5. How do you list Namespaces?

---

## Intermediate

6. Explain Namespace isolation.
7. Name the default Kubernetes namespaces.
8. How do you deploy resources into a specific Namespace?
9. What is the purpose of `kube-system`?
10. Why shouldn't production workloads use the default namespace?

---

## Advanced

11. Explain Namespace architecture.
12. How do Namespaces improve multi-tenancy?
13. What are Resource Quotas?
14. How does RBAC work with Namespaces?
15. How would you organize Namespaces for a large organization?

---

# 🎯 Practice Exercises

## Exercise 1

Create a namespace.

```bash
kubectl create namespace development
```

---

## Exercise 2

List all namespaces.

```bash
kubectl get namespaces
```

---

## Exercise 3

Deploy a Pod inside the development namespace.

```bash
kubectl apply -f pod.yaml -n development
```

---

## Exercise 4

View all resources inside a namespace.

```bash
kubectl get all -n development
```

---

## Exercise 5

Delete the namespace.

```bash
kubectl delete namespace development
```

---

# 🧩 Mini Project

Create a Markdown file named:

```text
kubernetes-namespaces-guide.md
```

Include:

- Namespace Overview
- Default Namespaces
- Namespace YAML
- Commands
- Resource Isolation
- Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add Kubernetes Namespaces guide"
```

---

# 📚 Further Reading

- Kubernetes Namespaces Documentation
- Kubernetes Resource Quotas
- Kubernetes RBAC
- Kubernetes API Reference

---

# 📚 Navigation

| ⬅️ Previous | 🏠 Home | ➡️ Next |
|------------|---------|---------|
| [07 - Deployments](07-Deployments.md) | [Kubernetes Roadmap](README.md) | [09 - Labels-and-Selectors.md](09-Labels-and-Selectors.md) |

---

# 🚀 What's Next?

In **Chapter 09 – Labels and Selectors**, you'll learn:

- 🏷️ What are Labels?
- 🎯 What are Selectors?
- 📝 Adding Labels
- 🔍 Filtering Resources
- 🏗️ Label Selectors
- 💻 kubectl Commands
- 🛠️ Best Practices
