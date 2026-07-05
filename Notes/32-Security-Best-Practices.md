# Kubernetes Notes
# Chapter 32 - Security Best Practices

> 📘 **Level:** Beginner to Advanced
> ⏱️ **Estimated Reading Time:** 75–90 minutes
> 🛠️ **Practice Time:** 4–5 hours

---

# 📚 Table of Contents

1. Kubernetes Security Overview
2. Why Security Matters
3. Security Layers
4. Cluster Security
5. Pod Security
6. Network Security
7. Secrets Management
8. Image Security
9. RBAC Best Practices
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

- Understand Kubernetes security fundamentals
- Secure clusters and workloads
- Protect sensitive data
- Implement RBAC effectively
- Follow production security best practices

---

# 📖 Kubernetes Security Overview

Kubernetes security involves protecting:

- Cluster infrastructure
- Worker nodes
- Containers
- Pods
- Applications
- Secrets
- Network communication

Security should be implemented at every layer of the cluster.

---

# 💡 Why Security Matters?

Without Security:

```text
Cluster

↓

Unauthorized Access

↓

Data Breach ❌
```

With Security:

```text
Secure Cluster

↓

Controlled Access

↓

Protected Applications ✅
```

Benefits:

- ✅ Protect sensitive data
- ✅ Prevent unauthorized access
- ✅ Reduce attack surface
- ✅ Improve compliance

---

# 🏗️ Kubernetes Security Layers

```text
Users

↓

Authentication

↓

Authorization (RBAC)

↓

Network Policies

↓

Pods

↓

Containers

↓

Nodes

↓

Cluster
```

---

# 🔐 Cluster Security

Protect the Kubernetes control plane by:

- Keeping Kubernetes updated
- Securing the API Server
- Restricting administrative access
- Enabling audit logs
- Using encrypted communication (TLS)

---

# 📦 Pod Security

Secure Pods by:

- Running containers as non-root
- Using read-only file systems where possible
- Dropping unnecessary Linux capabilities
- Avoiding privileged containers
- Defining security contexts

Example:

```yaml
securityContext:
  runAsNonRoot: true
  readOnlyRootFilesystem: true
```

---

# 🌐 Network Security

Use Network Policies to control traffic.

Recommendations:

- Allow only required communication
- Isolate sensitive workloads
- Restrict database access
- Secure namespace communication

---

# 🔑 Secrets Management

Never store passwords inside container images.

Use Kubernetes Secrets:

```bash
kubectl create secret generic db-secret \
--from-literal=password=MyPassword123
```

View Secrets:

```bash
kubectl get secrets
```

Best practices:

- Encrypt Secrets at rest.
- Rotate credentials regularly.
- Restrict Secret access using RBAC.

---

# 📦 Image Security

Use trusted container images.

Recommendations:

- Pull images from trusted registries
- Scan images for vulnerabilities
- Keep images updated
- Avoid unnecessary packages
- Use minimal base images

---

# 👤 RBAC Best Practices

Use Role-Based Access Control to limit permissions.

Recommendations:

- Follow the Principle of Least Privilege
- Avoid using `cluster-admin`
- Use Service Accounts
- Review permissions regularly
- Separate developer and administrator roles

---

# 💻 Useful Commands

View Pods:

```bash
kubectl get pods
```

View Secrets:

```bash
kubectl get secrets
```

View Roles:

```bash
kubectl get roles
```

View Network Policies:

```bash
kubectl get networkpolicy
```

Describe Pod:

```bash
kubectl describe pod nginx-pod
```

---

# 🏗️ Kubernetes Security Workflow

```text
User

↓

Authentication

↓

RBAC Authorization

↓

Network Policy

↓

Secure Pod

↓

Application
```

---

# 🏆 Best Practices

- ✅ Enable RBAC.
- ✅ Use Network Policies.
- ✅ Scan container images regularly.
- ✅ Run containers as non-root.
- ✅ Keep Kubernetes updated.
- ✅ Protect Secrets.
- ✅ Enable audit logging.
- ✅ Monitor cluster activity.

---

# 🌍 Common Security Controls

| Control | Purpose |
|----------|---------|
| RBAC | Access control |
| Network Policies | Network isolation |
| Secrets | Sensitive data storage |
| TLS | Secure communication |
| Security Context | Pod security |
| Image Scanning | Vulnerability detection |

---

# 🔄 Secure vs Insecure Cluster

| Secure Cluster | Insecure Cluster |
|----------------|------------------|
| RBAC Enabled | No Access Control |
| Network Policies | Open Network |
| Encrypted Secrets | Plain Text Secrets |
| Trusted Images | Unverified Images |
| Least Privilege | Full Access |

---

# 📝 Key Takeaways

- Security is a shared responsibility.
- Protect every layer of the Kubernetes cluster.
- Use RBAC and Network Policies.
- Secure Secrets and container images.
- Follow least privilege principles.

---

# 📋 Summary

In this chapter, you learned:

- Kubernetes Security
- Cluster Security
- Pod Security
- Network Security
- Secrets Management
- Image Security
- RBAC Best Practices

---

# ❓ Interview Questions

## Beginner

1. Why is Kubernetes security important?
2. What is RBAC?
3. What are Kubernetes Secrets?
4. What is a Network Policy?
5. Why should containers run as non-root?

---

## Intermediate

6. Explain Pod Security.
7. Why should privileged containers be avoided?
8. How do Network Policies improve security?
9. What are Security Contexts?
10. How do you secure Secrets?

---

## Advanced

11. Design a secure Kubernetes cluster.
12. Explain Kubernetes defense in depth.
13. How would you secure production workloads?
14. Why should container images be scanned?
15. Explain the Principle of Least Privilege.

---

# 🎯 Practice Exercises

## Exercise 1

List Kubernetes Secrets.

```bash
kubectl get secrets
```

---

## Exercise 2

View Network Policies.

```bash
kubectl get networkpolicy
```

---

## Exercise 3

List Roles.

```bash
kubectl get roles
```

---

## Exercise 4

Create a Secret.

```bash
kubectl create secret generic db-secret \
--from-literal=password=MyPassword123
```

---

## Exercise 5

Describe a Pod.

```bash
kubectl describe pod nginx-pod
```

---

# 🧩 Mini Project

Create a Markdown file named:

```text
kubernetes-security-guide.md
```

Include:

- Security Overview
- Cluster Security
- Pod Security
- Network Security
- Secrets
- RBAC
- Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add Kubernetes Security Best Practices guide"
```

---

# 📚 Further Reading

- Kubernetes Security Documentation
- Pod Security Standards
- Kubernetes RBAC Documentation
- Kubernetes Secrets Documentation
- Kubernetes Network Policies Documentation

---

# 📚 Navigation

| ⬅️ Previous | 🏠 Home | ➡️ Next |
|------------|---------|---------|
| [31 - Monitoring and Logging](31-Monitoring-and-Logging.md) | [Kubernetes Roadmap](README.md) | [33 - Kubernetes on AWS EKS](33-Kubernetes-on-AWS-EKS.md) |

---

# 🚀 What's Next?

In **Chapter 33 – Kubernetes on AWS EKS**, you'll learn:

- ☁️ What is Amazon EKS?
- 🏗️ EKS Architecture
- 🚀 Creating an EKS Cluster
- 👷 Managed Node Groups
- 💻 EKS Commands
- 🛠️ Best Practices
