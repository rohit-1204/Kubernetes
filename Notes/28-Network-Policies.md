# Kubernetes Notes
# Chapter 28 - Network Policies

> 📘 **Level:** Beginner to Intermediate
> ⏱️ **Estimated Reading Time:** 60–75 minutes
> 🛠️ **Practice Time:** 3–4 hours

---

# 📚 Table of Contents

1. What are Network Policies?
2. Why Use Network Policies?
3. Network Policy Architecture
4. Ingress and Egress
5. Pod Selectors
6. Network Policy YAML
7. Common Use Cases
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

- Understand Kubernetes Network Policies
- Control Pod communication
- Configure Ingress and Egress rules
- Improve cluster security
- Secure applications using network isolation

---

# 📖 What are Network Policies?

A **Network Policy** is a Kubernetes resource that controls **network traffic between Pods**.

By default, Pods can communicate freely within the cluster.

Network Policies define which Pods are allowed to communicate with each other.

---

# 💡 Why Use Network Policies?

Without Network Policies:

```text
Pod A

↓

Can Talk to

↓

All Pods ❌
```

With Network Policies:

```text
Pod A

↓

Allowed Pods Only

↓

Secure Communication ✅
```

Benefits:

- ✅ Better security
- ✅ Network isolation
- ✅ Least privilege networking
- ✅ Protect sensitive applications

---

# 🏗️ Network Policy Architecture

```text
          Client Pod

               │

               ▼

      Network Policy

               │

        Allow / Deny

               │

               ▼

        Target Pod
```

---

# 🌐 Ingress and Egress

## Ingress

Controls **incoming traffic** to a Pod.

```text
Incoming Request

↓

Ingress Rule

↓

Pod
```

---

## Egress

Controls **outgoing traffic** from a Pod.

```text
Pod

↓

Egress Rule

↓

External Service
```

---

# 🏷️ Pod Selectors

Network Policies use **labels** to select Pods.

Example:

```text
app=frontend

↓

Policy Applies

↓

Frontend Pods
```

---

# 📝 Network Policy YAML

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy

metadata:
  name: allow-frontend

spec:
  podSelector:
    matchLabels:
      app: frontend

  policyTypes:
    - Ingress

  ingress:
    - from:
        - podSelector:
            matchLabels:
              app: backend
```

Create the Network Policy:

```bash
kubectl apply -f network-policy.yaml
```

---

# 🌍 Common Use Cases

- Restrict database access
- Allow frontend to backend communication
- Block unwanted traffic
- Secure microservices
- Isolate namespaces

---

# 💻 Useful Commands

Create Network Policy:

```bash
kubectl apply -f network-policy.yaml
```

List Policies:

```bash
kubectl get networkpolicy
```

Describe Policy:

```bash
kubectl describe networkpolicy allow-frontend
```

Delete Policy:

```bash
kubectl delete networkpolicy allow-frontend
```

View Pods:

```bash
kubectl get pods --show-labels
```

---

# 🏗️ Network Policy Workflow

```text
Pod Sends Request

↓

Network Policy Evaluated

↓

Rule Matches?

↓

Yes → Traffic Allowed

No → Traffic Blocked
```

---

# 🏆 Best Practices

- ✅ Use Network Policies in production clusters.
- ✅ Apply the Principle of Least Privilege.
- ✅ Label Pods consistently.
- ✅ Test policies before deployment.
- ✅ Secure database Pods.
- ✅ Document network rules.

---

# 🌍 Common Use Cases

| Scenario | Network Policy |
|----------|----------------|
| Database Protection | ✅ |
| Microservices | ✅ |
| Namespace Isolation | ✅ |
| API Security | ✅ |
| Multi-Tenant Clusters | ✅ |

---

# 🔄 Ingress vs Egress

| Ingress | Egress |
|----------|---------|
| Controls incoming traffic | Controls outgoing traffic |
| Protects target Pods | Restricts destination access |
| Incoming connections | Outgoing connections |
| Most commonly used | Used for external communication control |

---

# 📝 Key Takeaways

- Network Policies control Pod communication.
- Ingress manages incoming traffic.
- Egress manages outgoing traffic.
- Policies use Pod labels for selection.
- They improve Kubernetes network security.

---

# 📋 Summary

In this chapter, you learned:

- Network Policies
- Ingress Rules
- Egress Rules
- Pod Selectors
- YAML Example
- Commands
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is a Network Policy?
2. Why are Network Policies used?
3. What is Ingress?
4. What is Egress?
5. How do you list Network Policies?

---

## Intermediate

6. Explain Pod Selectors.
7. Difference between Ingress and Egress?
8. How do Network Policies improve security?
9. What happens if no policy exists?
10. How do you create a Network Policy?

---

## Advanced

11. Explain Kubernetes network isolation.
12. How would you secure database Pods?
13. Why are labels important in Network Policies?
14. Explain communication between frontend and backend Pods.
15. Design secure networking for a production Kubernetes cluster.

---

# 🎯 Practice Exercises

## Exercise 1

Create a Network Policy.

---

## Exercise 2

List Network Policies.

```bash
kubectl get networkpolicy
```

---

## Exercise 3

Describe the Policy.

```bash
kubectl describe networkpolicy allow-frontend
```

---

## Exercise 4

Verify Pod labels.

```bash
kubectl get pods --show-labels
```

---

## Exercise 5

Delete the Policy.

```bash
kubectl delete networkpolicy allow-frontend
```

---

# 🧩 Mini Project

Create a Markdown file named:

```text
kubernetes-network-policies-guide.md
```

Include:

- Network Policy Overview
- Ingress
- Egress
- YAML Example
- Commands
- Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add Kubernetes Network Policies guide"
```

---

# 📚 Further Reading

- Kubernetes Network Policies Documentation
- Kubernetes Networking Concepts
- Kubernetes Security
- Kubernetes API Reference

---

# 📚 Navigation

| ⬅️ Previous | 🏠 Home | ➡️ Next |
|------------|---------|---------|
| [27 - Service Accounts](27-Service-Accounts.md) | [Kubernetes Roadmap](README.md) | [29 - Helm](29-Helm.md) |

---

# 🚀 What's Next?

In **Chapter 29 – Helm**, you'll learn:

- ⛵ What is Helm?
- 📦 Helm Charts
- 📁 Chart Structure
- 🚀 Installing Helm
- 🔄 Helm Releases
- 💻 Helm Commands
- 🛠️ Best Practices
