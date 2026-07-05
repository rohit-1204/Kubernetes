# Kubernetes Notes
# Chapter 25 - Rolling Updates and Rollbacks

> 📘 **Level:** Beginner to Intermediate
> ⏱️ **Estimated Reading Time:** 60–75 minutes
> 🛠️ **Practice Time:** 3–4 hours

---

# 📚 Table of Contents

1. What are Rolling Updates?
2. What are Rollbacks?
3. Why Use Rolling Updates?
4. Update Strategy
5. Rolling Update Architecture
6. Deployment YAML
7. Managing Updates
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

- Understand Rolling Updates
- Perform Rollbacks
- Update applications with zero downtime
- Manage Deployment revisions
- Monitor Deployment status

---

# 📖 What are Rolling Updates?

A **Rolling Update** is the default deployment strategy in Kubernetes.

Instead of stopping all existing Pods at once, Kubernetes gradually replaces old Pods with new ones.

This enables **zero or minimal downtime** during application updates.

---

# 📖 What is a Rollback?

A **Rollback** restores a Deployment to a previous stable version.

If a new application version fails, Kubernetes can quickly return to an earlier working revision.

---

# 💡 Why Use Rolling Updates?

Without Rolling Updates:

```text
Stop Old Pods

↓

Deploy New Pods

↓

Application Downtime ❌
```

With Rolling Updates:

```text
Old Pods Running

↓

New Pods Created

↓

Old Pods Removed

↓

No Downtime ✅
```

Benefits:

- ✅ Zero or minimal downtime
- ✅ Safer deployments
- ✅ Easy recovery
- ✅ Continuous application availability

---

# ⚙️ Update Strategy

Kubernetes supports different deployment strategies.

| Strategy | Description |
|----------|-------------|
| RollingUpdate | Gradually replaces Pods (Default) |
| Recreate | Stops all old Pods before creating new Pods |

---

# 🏗️ Rolling Update Architecture

```text
Deployment

      │

      ▼

Old ReplicaSet

      │

Rolling Update

      │

      ▼

New ReplicaSet

      │

      ▼

Updated Pods
```

---

# 📝 Deployment YAML

```yaml
apiVersion: apps/v1
kind: Deployment

metadata:
  name: nginx-deployment

spec:
  replicas: 3

  strategy:
    type: RollingUpdate

  selector:
    matchLabels:
      app: nginx

  template:
    metadata:
      labels:
        app: nginx

    spec:
      containers:
        - name: nginx
          image: nginx:latest
```

Apply the Deployment:

```bash
kubectl apply -f deployment.yaml
```

---

# 🔄 Managing Updates

Update an image:

```bash
kubectl set image deployment/nginx-deployment nginx=nginx:1.25
```

View rollout status:

```bash
kubectl rollout status deployment/nginx-deployment
```

View rollout history:

```bash
kubectl rollout history deployment/nginx-deployment
```

Rollback to the previous version:

```bash
kubectl rollout undo deployment/nginx-deployment
```

Rollback to a specific revision:

```bash
kubectl rollout undo deployment/nginx-deployment --to-revision=2
```

---

# 💻 Useful Commands

Create Deployment:

```bash
kubectl apply -f deployment.yaml
```

Update Image:

```bash
kubectl set image deployment/nginx-deployment nginx=nginx:1.25
```

Check Rollout Status:

```bash
kubectl rollout status deployment/nginx-deployment
```

View Rollout History:

```bash
kubectl rollout history deployment/nginx-deployment
```

Rollback Deployment:

```bash
kubectl rollout undo deployment/nginx-deployment
```

---

# 🏗️ Rolling Update Workflow

```text
New Image Available

↓

Deployment Updated

↓

New Pods Created

↓

Old Pods Terminated

↓

Application Updated
```

---

# 🏗️ Rollback Workflow

```text
Deployment Updated

↓

Application Fails

↓

Rollback Initiated

↓

Previous ReplicaSet Restored

↓

Application Running
```

---

# 🏆 Best Practices

- ✅ Use Rolling Updates for production deployments.
- ✅ Test applications before deployment.
- ✅ Monitor rollout progress.
- ✅ Keep Deployment revisions.
- ✅ Roll back immediately if issues occur.
- ✅ Use Readiness Probes for smooth updates.

---

# 🌍 Common Use Cases

| Scenario | Rolling Update |
|----------|----------------|
| Web Applications | ✅ |
| REST APIs | ✅ |
| Microservices | ✅ |
| Production Deployments | ✅ |
| Zero-Downtime Releases | ✅ |

---

# 🔄 Rolling Update vs Recreate

| Rolling Update | Recreate |
|---------------|----------|
| Zero or minimal downtime | Causes downtime |
| Gradual Pod replacement | Stops all Pods first |
| Recommended for production | Suitable for maintenance |
| Safer deployments | Simpler strategy |

---

# 📝 Key Takeaways

- Rolling Updates gradually replace old Pods.
- Rollbacks restore previous Deployment versions.
- Deployment history enables version recovery.
- Rolling Updates reduce downtime.
- Readiness Probes improve deployment safety.

---

# 📋 Summary

In this chapter, you learned:

- Rolling Updates
- Rollbacks
- Deployment Strategies
- Rollout Commands
- YAML Example
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is a Rolling Update?
2. What is a Rollback?
3. Why are Rolling Updates used?
4. What is the default Deployment strategy?
5. How do you check rollout status?

---

## Intermediate

6. Explain the Rolling Update process.
7. How do you update a Deployment image?
8. How do you perform a rollback?
9. What is rollout history?
10. Difference between RollingUpdate and Recreate?

---

## Advanced

11. How do Rolling Updates achieve zero downtime?
12. Why are Readiness Probes important during updates?
13. What happens if a deployment fails?
14. Explain Deployment revisions.
15. How would you safely deploy a new application version in production?

---

# 🎯 Practice Exercises

## Exercise 1

Create a Deployment.

---

## Exercise 2

Update the Deployment image.

```bash
kubectl set image deployment/nginx-deployment nginx=nginx:1.25
```

---

## Exercise 3

Monitor the rollout.

```bash
kubectl rollout status deployment/nginx-deployment
```

---

## Exercise 4

View rollout history.

```bash
kubectl rollout history deployment/nginx-deployment
```

---

## Exercise 5

Rollback the Deployment.

```bash
kubectl rollout undo deployment/nginx-deployment
```

---

# 🧩 Mini Project

Create a Markdown file named:

```text
kubernetes-rolling-updates-guide.md
```

Include:

- Rolling Updates
- Rollbacks
- Deployment Strategies
- YAML Example
- Commands
- Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add Kubernetes Rolling Updates guide"
```

---

# 📚 Further Reading

- Kubernetes Deployments Documentation
- Kubernetes Rollout Documentation
- Kubernetes Workloads
- Kubernetes API Reference

---

# 📚 Navigation

| ⬅️ Previous | 🏠 Home | ➡️ Next |
|------------|---------|---------|
| [24 - Horizontal Pod Autoscaler](24-Horizontal-Pod-Autoscaler.md) | [Kubernetes Roadmap](README.md) | [26 - RBAC](26-RBAC.md) |

---

# 🚀 What's Next?

In **Chapter 26 – RBAC (Role-Based Access Control)**, you'll learn:

- 🔐 What is RBAC?
- 👤 Users, Roles & Permissions
- 📋 Role and ClusterRole
- 🔗 RoleBinding & ClusterRoleBinding
- 💻 kubectl Commands
- 🛡️ Security Best Practices
