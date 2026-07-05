# Kubernetes Notes
# Chapter 29 - Helm

> 📘 **Level:** Beginner to Intermediate
> ⏱️ **Estimated Reading Time:** 75–90 minutes
> 🛠️ **Practice Time:** 4–5 hours

---

# 📚 Table of Contents

1. What is Helm?
2. Why Use Helm?
3. Helm Architecture
4. Installing Helm
5. Helm Charts
6. Chart Structure
7. Helm Repository
8. Helm Commands
9. Best Practices
10. Summary
11. Interview Questions
12. Practice Exercises
13. Mini Project
14. Further Reading

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Understand Helm
- Install Helm
- Work with Helm Charts
- Manage Helm Releases
- Deploy applications efficiently

---

# 📖 What is Helm?

**Helm** is the **package manager for Kubernetes**.

It simplifies deploying and managing Kubernetes applications using reusable packages called **Charts**.

Instead of manually creating multiple YAML files, Helm installs everything using a single command.

---

# 💡 Why Use Helm?

Without Helm:

```text
Application

↓

10+ YAML Files

↓

Manual Deployment ❌
```

With Helm:

```text
Helm Chart

↓

Single Command

↓

Application Deployed ✅
```

Benefits:

- ✅ Simplifies deployments
- ✅ Reusable templates
- ✅ Easy upgrades
- ✅ Easy rollbacks
- ✅ Version management

---

# 🏗️ Helm Architecture

```text
        Helm CLI

            │

            ▼

      Helm Chart

            │

            ▼

 Kubernetes API Server

            │

            ▼

      Kubernetes Cluster
```

---

# ⚙️ Installing Helm

Verify installation:

```bash
helm version
```

Add a repository:

```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
```

Update repositories:

```bash
helm repo update
```

Search charts:

```bash
helm search repo nginx
```

---

# 📦 What is a Helm Chart?

A **Helm Chart** is a collection of files that define a Kubernetes application.

A chart contains:

- Deployment
- Service
- ConfigMap
- Secret
- Ingress
- Other Kubernetes resources

Helm packages all of these into a reusable application template.

---

# 📁 Helm Chart Structure

```text
mychart/

├── Chart.yaml
├── values.yaml
├── charts/
├── templates/
│   ├── deployment.yaml
│   ├── service.yaml
│   ├── ingress.yaml
│   └── configmap.yaml
└── README.md
```

---

# 📄 Important Chart Files

| File | Purpose |
|------|---------|
| Chart.yaml | Chart metadata |
| values.yaml | Default configuration values |
| templates/ | Kubernetes YAML templates |
| charts/ | Dependent charts |
| README.md | Documentation |

---

# 🚀 Installing a Chart

Install NGINX from Bitnami:

```bash
helm install my-nginx bitnami/nginx
```

List installed releases:

```bash
helm list
```

View release status:

```bash
helm status my-nginx
```

---

# 🔄 Upgrading a Release

Upgrade using new values:

```bash
helm upgrade my-nginx bitnami/nginx
```

Rollback to the previous version:

```bash
helm rollback my-nginx 1
```

Uninstall the release:

```bash
helm uninstall my-nginx
```

---

# 💻 Useful Commands

Check Version:

```bash
helm version
```

Add Repository:

```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
```

Update Repository:

```bash
helm repo update
```

Search Charts:

```bash
helm search repo nginx
```

Install Chart:

```bash
helm install my-nginx bitnami/nginx
```

List Releases:

```bash
helm list
```

Upgrade Release:

```bash
helm upgrade my-nginx bitnami/nginx
```

Rollback Release:

```bash
helm rollback my-nginx 1
```

Delete Release:

```bash
helm uninstall my-nginx
```

---

# 🏗️ Helm Workflow

```text
Helm Chart

↓

helm install

↓

Kubernetes Resources Created

↓

Application Running

↓

helm upgrade

↓

Application Updated
```

---

# 🏆 Best Practices

- ✅ Store Charts in Git.
- ✅ Keep `values.yaml` environment-specific.
- ✅ Use official Helm repositories.
- ✅ Version your Charts.
- ✅ Test upgrades before production.
- ✅ Use `helm rollback` if deployments fail.

---

# 🌍 Common Use Cases

| Scenario | Helm |
|----------|------|
| NGINX Deployment | ✅ |
| Prometheus | ✅ |
| Grafana | ✅ |
| Jenkins | ✅ |
| WordPress | ✅ |

---

# 🔄 Kubernetes YAML vs Helm

| Kubernetes YAML | Helm |
|-----------------|------|
| Manual management | Automated deployment |
| Multiple files | Single Chart |
| Difficult upgrades | Easy upgrades |
| No versioning | Built-in release history |
| Harder to reuse | Reusable templates |

---

# 📝 Key Takeaways

- Helm is the package manager for Kubernetes.
- Helm uses Charts to package applications.
- Releases can be upgraded or rolled back easily.
- Charts simplify Kubernetes deployments.
- Helm is widely used in production environments.

---

# 📋 Summary

In this chapter, you learned:

- Helm
- Helm Charts
- Chart Structure
- Repositories
- Commands
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is Helm?
2. What is a Helm Chart?
3. Why do we use Helm?
4. How do you install a Chart?
5. How do you list installed releases?

---

## Intermediate

6. Explain the Helm architecture.
7. What is `values.yaml`?
8. Difference between a Chart and a Release?
9. How do you upgrade a Helm release?
10. How do you rollback a release?

---

## Advanced

11. Explain Helm templating.
12. Why is Helm preferred over plain YAML?
13. How would you deploy applications using Helm in production?
14. Explain Helm repositories.
15. How do Helm releases simplify application lifecycle management?

---

# 🎯 Practice Exercises

## Exercise 1

Install Helm.

---

## Exercise 2

Add the Bitnami repository.

```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
```

---

## Exercise 3

Search for NGINX.

```bash
helm search repo nginx
```

---

## Exercise 4

Install the NGINX Chart.

```bash
helm install my-nginx bitnami/nginx
```

---

## Exercise 5

Upgrade and rollback the release.

```bash
helm upgrade my-nginx bitnami/nginx

helm rollback my-nginx 1
```

---

# 🧩 Mini Project

Create a Markdown file named:

```text
kubernetes-helm-guide.md
```

Include:

- Helm Overview
- Chart Structure
- Repository Commands
- Installation
- Upgrade & Rollback
- Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add Kubernetes Helm guide"
```

---

# 📚 Further Reading

- Kubernetes Helm Documentation
- Helm Charts Documentation
- Bitnami Helm Charts
- Kubernetes Package Management

---

# 📚 Navigation

| ⬅️ Previous | 🏠 Home | ➡️ Next |
|------------|---------|---------|
| [28 - Network Policies](28-Network-Policies.md) | [Kubernetes Roadmap](README.md) | [30 - Kustomize](30-Kustomize.md) |

---

# 🚀 What's Next?

In **Chapter 30 – Kustomize**, you'll learn:

- 🧩 What is Kustomize?
- 📂 Base & Overlay Structure
- 📝 kustomization.yaml
- 🔄 Environment-specific Configurations
- 💻 Kustomize Commands
- 🛠️ Best Practices
