# Kubernetes Notes
# Chapter 26 - RBAC (Role-Based Access Control)

> 📘 **Level:** Beginner to Intermediate
> ⏱️ **Estimated Reading Time:** 60–75 minutes
> 🛠️ **Practice Time:** 3–4 hours

---

# 📚 Table of Contents

1. What is RBAC?
2. Why Use RBAC?
3. RBAC Components
4. RBAC Architecture
5. Roles and ClusterRoles
6. RoleBindings and ClusterRoleBindings
7. RBAC YAML Examples
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

- Understand Kubernetes RBAC
- Create Roles and ClusterRoles
- Assign permissions using RoleBindings
- Secure Kubernetes resources
- Follow the Principle of Least Privilege

---

# 📖 What is RBAC?

**Role-Based Access Control (RBAC)** is Kubernetes' authorization mechanism that controls **who can perform which actions on which resources**.

RBAC helps secure a Kubernetes cluster by granting only the required permissions.

Example:

```text
User

↓

Role

↓

Permissions

↓

Kubernetes Resources
```

---

# 💡 Why Use RBAC?

Without RBAC:

```text
User

↓

Full Cluster Access ❌
```

With RBAC:

```text
User

↓

Limited Permissions

↓

Authorized Resources Only ✅
```

Benefits:

- ✅ Improved security
- ✅ Controlled access
- ✅ Least privilege
- ✅ Easier permission management

---

# 🏗️ RBAC Components

| Component | Purpose |
|-----------|---------|
| Role | Permissions within a namespace |
| ClusterRole | Permissions across the entire cluster |
| RoleBinding | Assigns a Role to a user, group, or ServiceAccount |
| ClusterRoleBinding | Assigns a ClusterRole cluster-wide |

---

# 🏗️ RBAC Architecture

```text
          User / ServiceAccount

                  │

                  ▼

         RoleBinding

                  │

                  ▼

         Role / ClusterRole

                  │

                  ▼

        Kubernetes Resources
```

---

# 📋 Role

A **Role** defines permissions within a **single namespace**.

Example:

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role

metadata:
  name: pod-reader
  namespace: default

rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "list", "watch"]
```

Create the Role:

```bash
kubectl apply -f role.yaml
```

---

# 🌍 ClusterRole

A **ClusterRole** defines permissions across the entire cluster.

Example:

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole

metadata:
  name: pod-reader

rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "list", "watch"]
```

---

# 🔗 RoleBinding

A **RoleBinding** grants a Role to a user or ServiceAccount within a namespace.

Example:

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding

metadata:
  name: read-pods

subjects:
- kind: ServiceAccount
  name: app-sa
  namespace: default

roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```

---

# 🌐 ClusterRoleBinding

A **ClusterRoleBinding** grants a ClusterRole across the cluster.

Example:

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding

metadata:
  name: cluster-read

subjects:
- kind: ServiceAccount
  name: app-sa
  namespace: default

roleRef:
  kind: ClusterRole
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```

---

# 💻 Useful Commands

Create RBAC resources:

```bash
kubectl apply -f role.yaml
```

List Roles:

```bash
kubectl get roles
```

List ClusterRoles:

```bash
kubectl get clusterroles
```

List RoleBindings:

```bash
kubectl get rolebindings
```

List ClusterRoleBindings:

```bash
kubectl get clusterrolebindings
```

Describe a Role:

```bash
kubectl describe role pod-reader
```

---

# 🏗️ RBAC Workflow

```text
User / ServiceAccount

↓

RoleBinding

↓

Role

↓

Permission Check

↓

Access Granted or Denied
```

---

# 🏆 Best Practices

- ✅ Follow the Principle of Least Privilege.
- ✅ Prefer Roles over ClusterRoles whenever possible.
- ✅ Use ServiceAccounts instead of default credentials.
- ✅ Review permissions regularly.
- ✅ Avoid granting `cluster-admin` unless necessary.
- ✅ Store RBAC manifests in Git.

---

# 🌍 Common Use Cases

| Scenario | RBAC |
|----------|------|
| Developer Access | ✅ |
| Read-Only Access | ✅ |
| CI/CD Pipelines | ✅ |
| Monitoring Tools | ✅ |
| Application ServiceAccounts | ✅ |

---

# 🔄 Role vs ClusterRole

| Role | ClusterRole |
|------|-------------|
| Namespace-scoped | Cluster-scoped |
| Limited to one namespace | Works across all namespaces |
| Used with RoleBinding | Used with ClusterRoleBinding |
| Preferred for most workloads | Used for cluster-wide permissions |

---

# 📝 Key Takeaways

- RBAC controls access to Kubernetes resources.
- Roles are namespace-specific.
- ClusterRoles provide cluster-wide permissions.
- RoleBindings connect users or ServiceAccounts to Roles.
- RBAC is essential for Kubernetes security.

---

# 📋 Summary

In this chapter, you learned:

- RBAC
- Roles
- ClusterRoles
- RoleBindings
- ClusterRoleBindings
- YAML Examples
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is RBAC?
2. Why is RBAC important?
3. What is a Role?
4. What is a RoleBinding?
5. What is a ClusterRole?

---

## Intermediate

6. Difference between Role and ClusterRole?
7. Difference between RoleBinding and ClusterRoleBinding?
8. Why should ServiceAccounts be used?
9. Explain the Principle of Least Privilege.
10. How do you list Roles?

---

## Advanced

11. Explain Kubernetes authorization using RBAC.
12. How would you provide read-only access to developers?
13. Why should `cluster-admin` be avoided?
14. How do RoleBindings work?
15. Design RBAC for a production Kubernetes cluster.

---

# 🎯 Practice Exercises

## Exercise 1

Create a Role.

---

## Exercise 2

Create a RoleBinding.

---

## Exercise 3

List all Roles.

```bash
kubectl get roles
```

---

## Exercise 4

Describe the Role.

```bash
kubectl describe role pod-reader
```

---

## Exercise 5

Create a ClusterRole and ClusterRoleBinding.

---

# 🧩 Mini Project

Create a Markdown file named:

```text
kubernetes-rbac-guide.md
```

Include:

- RBAC Overview
- Roles
- ClusterRoles
- RoleBindings
- ClusterRoleBindings
- Commands
- Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add Kubernetes RBAC guide"
```

---

# 📚 Further Reading

- Kubernetes RBAC Documentation
- Kubernetes Authorization
- Kubernetes Security
- Kubernetes API Reference

---

# 📚 Navigation

| ⬅️ Previous | 🏠 Home | ➡️ Next |
|------------|---------|---------|
| [25 - Rolling Updates and Rollbacks](25-Rolling-Updates-and-Rollbacks.md) | [Kubernetes Roadmap](README.md) | [27 - Service Accounts](27-Service-Accounts.md) |

---

# 🚀 What's Next?

In **Chapter 27 – Service Accounts**, you'll learn:

- 👤 What are Service Accounts?
- 🔑 Authentication in Kubernetes
- 🛡️ ServiceAccount Tokens
- 📝 YAML Examples
- 💻 kubectl Commands
- 🏗️ Best Practices
