# Kubernetes Notes
# Chapter 14 - Secrets

> 📘 **Level:** Beginner
> ⏱️ **Estimated Reading Time:** 50–60 minutes
> 🛠️ **Practice Time:** 2–3 hours

---

# 📚 Table of Contents

1. What are Secrets?
2. Why Use Secrets?
3. Secret Architecture
4. Types of Secrets
5. Creating Secrets
6. Secret YAML
7. Using Secrets
8. Mounting Secrets
9. Managing Secrets
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

- Understand Kubernetes Secrets
- Store sensitive information securely
- Create and manage Secrets
- Use Secrets as environment variables
- Mount Secrets as files inside containers

---

# 📖 What are Secrets?

A **Secret** is a Kubernetes resource used to store **sensitive information** such as:

- Passwords
- API Keys
- Database Credentials
- OAuth Tokens
- TLS Certificates

Secrets help separate confidential data from application code.

---

# 💡 Why Use Secrets?

Without Secrets:

```text
Application

↓

Password Inside Code

↓

Security Risk ❌
```

With Secrets:

```text
Application

↓

Kubernetes Secret

↓

Password Loaded Securely

↓

Safer Deployment ✅
```

Benefits:

- ✅ Secure storage
- ✅ Separate secrets from code
- ✅ Easy management
- ✅ Reusable across applications

---

# 🏗️ Secret Architecture

```text
          Secret
             │
     ┌───────┴────────┐
     ▼                ▼
Environment      Mounted File
 Variables
             │
             ▼
            Pod
```

---

# 🔐 Types of Secrets

| Secret Type | Purpose |
|-------------|----------|
| Opaque | Generic key-value data |
| kubernetes.io/tls | TLS certificates |
| kubernetes.io/dockerconfigjson | Docker registry credentials |
| kubernetes.io/basic-auth | Username and password |
| kubernetes.io/service-account-token | Service Account token |

---

# 🚀 Creating Secrets

Create a generic Secret:

```bash
kubectl create secret generic app-secret \
--from-literal=username=admin \
--from-literal=password=Password123
```

List Secrets:

```bash
kubectl get secrets
```

---

# 📝 Secret YAML

```yaml
apiVersion: v1
kind: Secret

metadata:
  name: app-secret

type: Opaque

stringData:
  username: admin
  password: Password123
```

Create the Secret:

```bash
kubectl apply -f secret.yaml
```

---

# 🌍 Using Secrets

Use a Secret as an environment variable:

```yaml
env:
  - name: DB_PASSWORD
    valueFrom:
      secretKeyRef:
        name: app-secret
        key: password
```

The application can access the password through an environment variable.

---

# 📂 Mounting Secrets

Secrets can also be mounted as files.

```yaml
volumes:
  - name: secret-volume
    secret:
      secretName: app-secret
```

Mount inside the container:

```yaml
volumeMounts:
  - name: secret-volume
    mountPath: /etc/secrets
```

The Secret becomes available as files inside the container.

---

# ⚙️ Managing Secrets

Describe a Secret:

```bash
kubectl describe secret app-secret
```

View Secret YAML:

```bash
kubectl get secret app-secret -o yaml
```

Delete Secret:

```bash
kubectl delete secret app-secret
```

---

# 💻 Useful Commands

Create Secret:

```bash
kubectl create secret generic app-secret \
--from-literal=password=Password123
```

List Secrets:

```bash
kubectl get secrets
```

Describe Secret:

```bash
kubectl describe secret app-secret
```

View YAML:

```bash
kubectl get secret app-secret -o yaml
```

Delete Secret:

```bash
kubectl delete secret app-secret
```

---

# 🏗️ Secret Workflow

```text
Create Secret

↓

Store Sensitive Data

↓

Reference in Pod

↓

Application Reads Secret
```

---

# 🏆 Best Practices

- ✅ Store only sensitive data.
- ✅ Use RBAC to restrict access.
- ✅ Rotate secrets regularly.
- ✅ Never store secrets in Git repositories.
- ✅ Use external secret managers for production when possible.
- ✅ Encrypt Secrets at rest.

---

# 🌍 Common Use Cases

| Use Case | Secret |
|----------|--------|
| Database Password | ✅ |
| API Key | ✅ |
| OAuth Token | ✅ |
| TLS Certificate | ✅ |
| Docker Registry Login | ✅ |

---

# 🔄 Secret vs ConfigMap

| Secret | ConfigMap |
|---------|-----------|
| Sensitive information | Non-sensitive configuration |
| Passwords, Tokens | URLs, App Settings |
| Restricted access | General configuration |
| Better security | Easy configuration management |

---

# 📝 Key Takeaways

- Secrets store sensitive information securely.
- Secrets should replace hardcoded credentials.
- Secrets can be used as environment variables or mounted as files.
- RBAC helps protect Secret access.
- Secrets improve application security.

---

# 📋 Summary

In this chapter, you learned:

- Kubernetes Secrets
- Secret Types
- Secret YAML
- Environment Variables
- Mounted Files
- Commands
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is a Kubernetes Secret?
2. Why do we use Secrets?
3. What type of data should be stored in Secrets?
4. How do you create a Secret?
5. How do you list Secrets?

---

## Intermediate

6. Explain Secret architecture.
7. How do you use Secrets inside a Pod?
8. Difference between Secret and ConfigMap?
9. What are Secret types?
10. How do you mount a Secret?

---

## Advanced

11. How do Secrets improve application security?
12. Explain Secret encryption at rest.
13. How would you rotate Secrets in production?
14. How does RBAC protect Secrets?
15. What are best practices for managing Secrets?

---

# 🎯 Practice Exercises

## Exercise 1

Create a Secret.

---

## Exercise 2

List all Secrets.

```bash
kubectl get secrets
```

---

## Exercise 3

Use a Secret as an environment variable.

---

## Exercise 4

Mount a Secret as a volume.

---

## Exercise 5

Delete the Secret.

```bash
kubectl delete secret app-secret
```

---

# 🧩 Mini Project

Create a Markdown file named:

```text
kubernetes-secrets-guide.md
```

Include:

- Secret Overview
- Secret Types
- YAML Example
- Environment Variables
- Mounted Secrets
- Commands
- Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add Kubernetes Secrets guide"
```

---

# 📚 Further Reading

- Kubernetes Secrets Documentation
- Kubernetes Security Best Practices
- Kubernetes API Reference
- kubectl Documentation

---

# 📚 Navigation

| ⬅️ Previous | 🏠 Home | ➡️ Next |
|------------|---------|---------|
| [13 - ConfigMaps](13-ConfigMaps.md) | [Kubernetes Roadmap](README.md) | [15 - PersistentVolumes.md](15-PersistentVolumes.md) |

---

# 🚀 What's Next?

In **Chapter 15 – Persistent Volumes**, you'll learn:

- 💾 What is Persistent Storage?
- 📦 Persistent Volumes (PV)
- 📂 Persistent Volume Claims (PVC)
- 📝 PV & PVC YAML
- 🔄 Storage Classes
- 💻 Storage Commands
- 🛠️ Best Practices
