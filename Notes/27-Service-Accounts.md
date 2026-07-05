# Kubernetes Notes
# Chapter 27 - Service Accounts

> 📘 **Level:** Beginner to Intermediate
> ⏱️ **Estimated Reading Time:** 50–65 minutes
> 🛠️ **Practice Time:** 2–3 hours

---

# 📚 Table of Contents

1. What is a Service Account?
2. Why Use Service Accounts?
3. Service Account Architecture
4. Default Service Account
5. Creating a Service Account
6. Using a Service Account
7. RBAC Integration
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

- Understand Kubernetes Service Accounts
- Create and manage Service Accounts
- Assign Service Accounts to Pods
- Integrate Service Accounts with RBAC
- Secure application access to the Kubernetes API

---

# 📖 What is a Service Account?

A **Service Account** is an identity used by **applications and Pods** running inside a Kubernetes cluster.

Unlike a regular user account, a Service Account is designed for workloads instead of people.

Applications use Service Accounts to securely communicate with the Kubernetes API.

---

# 💡 Why Use Service Accounts?

Without Service Account:

```text
Application

↓

No Identity

↓

Cannot Access Kubernetes API ❌
```

With Service Account:

```text
Application

↓

Service Account

↓

Authenticated

↓

Access Granted ✅
```

Benefits:

- ✅ Secure authentication
- ✅ Fine-grained permissions
- ✅ Works with RBAC
- ✅ Supports automation

---

# 🏗️ Service Account Architecture

```text
          Pod

           │

           ▼

   Service Account

           │

           ▼

      API Server

           │

           ▼

     RBAC Authorization
```

---

# 👤 Default Service Account

Every namespace automatically contains a **default Service Account**.

If a Pod does not specify one, Kubernetes assigns the default Service Account automatically.

Example:

```text
Namespace

↓

Default Service Account

↓

Pod Uses Default
```

---

# 📝 Creating a Service Account

YAML Example:

```yaml
apiVersion: v1
kind: ServiceAccount

metadata:
  name: app-sa
```

Create the Service Account:

```bash
kubectl apply -f serviceaccount.yaml
```

---

# 🚀 Using a Service Account

Assign a Service Account to a Pod:

```yaml
apiVersion: v1
kind: Pod

metadata:
  name: nginx-pod

spec:
  serviceAccountName: app-sa

  containers:
    - name: nginx
      image: nginx
```

Create the Pod:

```bash
kubectl apply -f pod.yaml
```

---

# 🔐 RBAC Integration

Service Accounts are commonly used with RBAC.

Workflow:

```text
Service Account

↓

RoleBinding

↓

Role

↓

Permissions

↓

Kubernetes API
```

This ensures applications receive only the permissions they require.

---

# 💻 Useful Commands

Create Service Account:

```bash
kubectl apply -f serviceaccount.yaml
```

List Service Accounts:

```bash
kubectl get serviceaccounts
```

Describe Service Account:

```bash
kubectl describe serviceaccount app-sa
```

Delete Service Account:

```bash
kubectl delete serviceaccount app-sa
```

View Pod:

```bash
kubectl describe pod nginx-pod
```

---

# 🏗️ Service Account Workflow

```text
Pod Created

↓

Service Account Assigned

↓

Authentication

↓

RBAC Check

↓

API Access
```

---

# 🏆 Best Practices

- ✅ Create dedicated Service Accounts for applications.
- ✅ Avoid using the default Service Account in production.
- ✅ Grant only required permissions.
- ✅ Use RBAC with Service Accounts.
- ✅ Review Service Account permissions regularly.
- ✅ Store YAML manifests in Git.

---

# 🌍 Common Use Cases

| Scenario | Service Account |
|----------|-----------------|
| CI/CD Pipeline | ✅ |
| Monitoring Tools | ✅ |
| Operators | ✅ |
| Controllers | ✅ |
| Custom Applications | ✅ |

---

# 🔄 User Account vs Service Account

| User Account | Service Account |
|--------------|-----------------|
| Used by humans | Used by Pods and applications |
| External authentication | Managed by Kubernetes |
| Manual login | Automatic authentication |
| Interactive access | Application access |

---

# 📝 Key Takeaways

- Service Accounts provide identities for Pods.
- Every namespace has a default Service Account.
- Service Accounts work closely with RBAC.
- Dedicated Service Accounts improve security.
- They enable secure communication with the Kubernetes API.

---

# 📋 Summary

In this chapter, you learned:

- Service Accounts
- Default Service Account
- YAML Examples
- RBAC Integration
- Commands
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is a Service Account?
2. Why do Pods use Service Accounts?
3. What is the default Service Account?
4. How do you create a Service Account?
5. How do you list Service Accounts?

---

## Intermediate

6. Explain Service Account authentication.
7. How does RBAC work with Service Accounts?
8. Why shouldn't production workloads use the default Service Account?
9. How do you assign a Service Account to a Pod?
10. What is the purpose of `serviceAccountName`?

---

## Advanced

11. Explain how Service Accounts authenticate with the Kubernetes API.
12. How would you secure application access using RBAC?
13. Why should each application have its own Service Account?
14. Explain the relationship between Service Accounts and Roles.
15. Design secure Service Account access for a production cluster.

---

# 🎯 Practice Exercises

## Exercise 1

Create a Service Account.

---

## Exercise 2

Assign the Service Account to a Pod.

---

## Exercise 3

Verify the Service Account.

```bash
kubectl get serviceaccounts
```

---

## Exercise 4

Describe the Service Account.

```bash
kubectl describe serviceaccount app-sa
```

---

## Exercise 5

Create a Role and RoleBinding for the Service Account.

---

# 🧩 Mini Project

Create a Markdown file named:

```text
kubernetes-service-accounts-guide.md
```

Include:

- Service Account Overview
- Default Service Account
- YAML Examples
- RBAC Integration
- Commands
- Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add Kubernetes Service Accounts guide"
```

---

# 📚 Further Reading

- Kubernetes Service Accounts Documentation
- Kubernetes Authentication
- Kubernetes RBAC Documentation
- Kubernetes API Reference

---

# 📚 Navigation

| ⬅️ Previous | 🏠 Home | ➡️ Next |
|------------|---------|---------|
| [26 - RBAC](26-RBAC.md) | [Kubernetes Roadmap](README.md) | [28 - Network Policies](28-Network-Policies.md) |

---

# 🚀 What's Next?

In **Chapter 28 – Network Policies**, you'll learn:

- 🌐 What are Network Policies?
- 🔒 Controlling Pod-to-Pod Communication
- 📜 Network Policy YAML
- 🚦 Ingress & Egress Rules
- 💻 kubectl Commands
- 🛡️ Security Best Practices
