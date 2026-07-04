# Kubernetes Notes
# Chapter 13 - ConfigMaps

> 📘 **Level:** Beginner
> ⏱️ **Estimated Reading Time:** 50–60 minutes
> 🛠️ **Practice Time:** 2–3 hours

---

# 📚 Table of Contents

1. What is a ConfigMap?
2. Why Use ConfigMaps?
3. ConfigMap Architecture
4. Creating ConfigMaps
5. ConfigMap YAML
6. Using ConfigMaps
7. Mounting ConfigMaps
8. Managing ConfigMaps
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

- Understand ConfigMaps
- Store application configuration
- Use ConfigMaps as environment variables
- Mount ConfigMaps as files
- Manage ConfigMaps using kubectl

---

# 📖 What is a ConfigMap?

A **ConfigMap** is a Kubernetes resource used to store **non-sensitive configuration data** as key-value pairs.

Instead of hardcoding configuration inside a container image, you can store it in a ConfigMap and use it when the application starts.

Examples:

- Application settings
- Environment names
- URLs
- Configuration files

> **Note:** Do not store passwords, API keys, or secrets in ConfigMaps. Use **Secrets** instead.

---

# 💡 Why Use ConfigMaps?

Without ConfigMaps:

```text
Application

↓

Configuration Inside Image

↓

Rebuild Image for Every Change ❌
```

With ConfigMaps:

```text
Application

↓

ConfigMap

↓

Configuration Loaded

↓

No Image Rebuild ✅
```

Benefits:

- ✅ Separate configuration from code
- ✅ Easy updates
- ✅ Reusable configuration
- ✅ Better application management

---

# 🏗️ ConfigMap Architecture

```text
          ConfigMap
               │
      ┌────────┴────────┐
      ▼                 ▼
Environment Variables   Mounted Files
               │
               ▼
             Pod
```

---

# 🚀 Creating ConfigMaps

Create from literal values:

```bash
kubectl create configmap app-config \
--from-literal=APP_NAME=myapp \
--from-literal=ENV=production
```

Create from a file:

```bash
kubectl create configmap app-config \
--from-file=config.properties
```

List ConfigMaps:

```bash
kubectl get configmaps
```

---

# 📝 ConfigMap YAML

```yaml
apiVersion: v1
kind: ConfigMap

metadata:
  name: app-config

data:
  APP_NAME: myapp
  ENV: production
```

Create the ConfigMap:

```bash
kubectl apply -f configmap.yaml
```

---

# 🌍 Using ConfigMaps

Use ConfigMap as environment variables:

```yaml
env:
  - name: APP_NAME
    valueFrom:
      configMapKeyRef:
        name: app-config
        key: APP_NAME
```

The application can now read the environment variable.

---

# 📂 Mounting ConfigMaps

ConfigMaps can also be mounted as files.

Example:

```yaml
volumes:
  - name: config-volume
    configMap:
      name: app-config
```

Then mount it inside the container:

```yaml
volumeMounts:
  - name: config-volume
    mountPath: /etc/config
```

The configuration becomes available as files.

---

# ⚙️ Managing ConfigMaps

Describe a ConfigMap:

```bash
kubectl describe configmap app-config
```

View ConfigMap YAML:

```bash
kubectl get configmap app-config -o yaml
```

Delete ConfigMap:

```bash
kubectl delete configmap app-config
```

---

# 💻 Useful Commands

Create ConfigMap:

```bash
kubectl create configmap app-config \
--from-literal=ENV=production
```

List ConfigMaps:

```bash
kubectl get configmaps
```

Describe ConfigMap:

```bash
kubectl describe configmap app-config
```

View YAML:

```bash
kubectl get configmap app-config -o yaml
```

Delete ConfigMap:

```bash
kubectl delete configmap app-config
```

---

# 🏗️ ConfigMap Workflow

```text
Create ConfigMap

↓

Store Configuration

↓

Reference in Pod

↓

Application Reads Configuration
```

---

# 🏆 Best Practices

- ✅ Store only non-sensitive data.
- ✅ Use Secrets for passwords and API keys.
- ✅ Keep configuration separate from application code.
- ✅ Use meaningful ConfigMap names.
- ✅ Version configuration files.
- ✅ Store YAML manifests in Git.

---

# 🌍 Common Use Cases

| Use Case | ConfigMap |
|----------|-----------|
| Application Settings | ✅ |
| Environment Variables | ✅ |
| URLs | ✅ |
| Configuration Files | ✅ |
| Feature Flags | ✅ |

---

# 🔄 ConfigMap vs Secret

| ConfigMap | Secret |
|-----------|---------|
| Stores non-sensitive data | Stores sensitive data |
| Plain text | Base64 encoded |
| Configuration | Passwords, Tokens, Keys |
| Easy to read | Restricted access |

---

# 📝 Key Takeaways

- ConfigMaps store non-sensitive configuration.
- Configuration is separated from application code.
- ConfigMaps can be used as environment variables or mounted as files.
- Secrets should be used for sensitive information.
- ConfigMaps simplify application configuration management.

---

# 📋 Summary

In this chapter, you learned:

- ConfigMaps
- ConfigMap YAML
- Environment Variables
- Mounted Files
- Commands
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is a ConfigMap?
2. Why are ConfigMaps used?
3. Can ConfigMaps store passwords?
4. How do you create a ConfigMap?
5. How do you list ConfigMaps?

---

## Intermediate

6. Explain ConfigMap architecture.
7. How do you use ConfigMaps as environment variables?
8. How do you mount a ConfigMap?
9. Difference between ConfigMap and Secret?
10. When should ConfigMaps be used?

---

## Advanced

11. Explain how ConfigMaps improve application deployment.
12. How would you update configuration without rebuilding a container image?
13. What happens when a ConfigMap is modified?
14. How would you organize ConfigMaps in production?
15. What are the limitations of ConfigMaps?

---

# 🎯 Practice Exercises

## Exercise 1

Create a ConfigMap.

---

## Exercise 2

View ConfigMaps.

```bash
kubectl get configmaps
```

---

## Exercise 3

Use a ConfigMap as an environment variable.

---

## Exercise 4

Mount a ConfigMap as a volume.

---

## Exercise 5

Delete the ConfigMap.

```bash
kubectl delete configmap app-config
```

---

# 🧩 Mini Project

Create a Markdown file named:

```text
kubernetes-configmaps-guide.md
```

Include:

- ConfigMap Overview
- YAML Example
- Environment Variables
- Mounted Files
- Commands
- Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add Kubernetes ConfigMaps guide"
```

---

# 📚 Further Reading

- Kubernetes ConfigMap Documentation
- Kubernetes Configuration Management
- Kubernetes API Reference
- kubectl Documentation

---

# 📚 Navigation

| ⬅️ Previous | 🏠 Home | ➡️ Next |
|------------|---------|---------|
| [12 - Ingress](12-Ingress.md) | [Kubernetes Roadmap](README.md) | [14 - Secrets.md](14-Secrets.md) |

---

# 🚀 What's Next?

In **Chapter 14 – Secrets**, you'll learn:

- 🔐 What are Kubernetes Secrets?
- 📝 Creating Secrets
- 🌍 Using Secrets in Pods
- 📂 Mounting Secrets
- 🔒 Secret Types
- 💻 Secret Commands
- 🛠️ Best Practices
