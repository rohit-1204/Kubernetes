# Kubernetes Notes
# Chapter 16 - Persistent Volume Claims (PVC)

> 📘 **Level:** Beginner
> ⏱️ **Estimated Reading Time:** 45–60 minutes
> 🛠️ **Practice Time:** 2–3 hours

---

# 📚 Table of Contents

1. What is a Persistent Volume Claim?
2. Why Use PVC?
3. PVC Architecture
4. PVC Components
5. PVC YAML
6. Using PVC in Pods
7. Access Modes
8. Storage Classes
9. Managing PVCs
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

- Understand Persistent Volume Claims (PVC)
- Request storage for applications
- Mount PVCs inside Pods
- Understand Access Modes
- Manage PVCs using kubectl

---

# 📖 What is a Persistent Volume Claim (PVC)?

A **Persistent Volume Claim (PVC)** is a request for storage made by a Kubernetes application.

Instead of directly using a Persistent Volume (PV), Pods request storage through a PVC.

Kubernetes automatically binds the PVC to a matching Persistent Volume.

---

# 💡 Why Use PVC?

Without PVC:

```text
Pod

↓

Directly Uses PV

↓

Difficult to Manage ❌
```

With PVC:

```text
Pod

↓

Persistent Volume Claim

↓

Persistent Volume

↓

Storage ✅
```

Benefits:

- ✅ Storage abstraction
- ✅ Easier management
- ✅ Automatic PV binding
- ✅ Portable application manifests

---

# 🏗️ PVC Architecture

```text
          Application

               │

               ▼

              Pod

               │

               ▼

Persistent Volume Claim

               │

               ▼

      Persistent Volume

               │

               ▼

     Physical Storage
```

---

# 📦 PVC Components

A PVC defines:

- Requested storage size
- Access mode
- Storage class (optional)

Example:

```text
Storage: 10Gi

Access Mode: ReadWriteOnce
```

---

# 📝 PVC YAML

```yaml
apiVersion: v1
kind: PersistentVolumeClaim

metadata:
  name: app-pvc

spec:
  accessModes:
    - ReadWriteOnce

  resources:
    requests:
      storage: 5Gi
```

Create the PVC:

```bash
kubectl apply -f pvc.yaml
```

---

# 🌍 Using PVC in Pods

Example Pod:

```yaml
apiVersion: v1
kind: Pod

metadata:
  name: nginx-pod

spec:
  containers:
    - name: nginx
      image: nginx

      volumeMounts:
        - name: storage
          mountPath: /data

  volumes:
    - name: storage
      persistentVolumeClaim:
        claimName: app-pvc
```

The Pod now stores data using the Persistent Volume.

---

# 🔄 Access Modes

| Access Mode | Description |
|-------------|-------------|
| ReadWriteOnce (RWO) | Mounted by one node with read/write access |
| ReadOnlyMany (ROX) | Mounted by many nodes with read-only access |
| ReadWriteMany (RWX) | Mounted by many nodes with read/write access |
| ReadWriteOncePod (RWOP) | Mounted by only one Pod |

---

# ☁️ Storage Classes

A **StorageClass** enables **dynamic provisioning** of storage.

Benefits:

- ✅ Automatic volume creation
- ✅ No manual PV creation
- ✅ Cloud provider integration
- ✅ Easier storage management

---

# ⚙️ Managing PVCs

List PVCs:

```bash
kubectl get pvc
```

Describe a PVC:

```bash
kubectl describe pvc app-pvc
```

View YAML:

```bash
kubectl get pvc app-pvc -o yaml
```

Delete PVC:

```bash
kubectl delete pvc app-pvc
```

---

# 💻 Useful Commands

Create PVC:

```bash
kubectl apply -f pvc.yaml
```

List PVCs:

```bash
kubectl get pvc
```

Describe PVC:

```bash
kubectl describe pvc app-pvc
```

View YAML:

```bash
kubectl get pvc app-pvc -o yaml
```

Delete PVC:

```bash
kubectl delete pvc app-pvc
```

---

# 🏗️ PVC Workflow

```text
Create PVC

↓

Request Storage

↓

PVC Binds to PV

↓

Pod Mounts PVC

↓

Persistent Data
```

---

# 🏆 Best Practices

- ✅ Use Storage Classes whenever possible.
- ✅ Request only the storage you need.
- ✅ Choose the correct access mode.
- ✅ Monitor storage usage.
- ✅ Use meaningful PVC names.
- ✅ Back up persistent data regularly.

---

# 🌍 Common Use Cases

| Scenario | PVC |
|----------|-----|
| Database Storage | ✅ |
| File Uploads | ✅ |
| Application Data | ✅ |
| CMS Storage | ✅ |
| Shared Files | ✅ |

---

# 🔄 PV vs PVC

| Persistent Volume (PV) | Persistent Volume Claim (PVC) |
|-------------------------|-------------------------------|
| Provides storage | Requests storage |
| Created by admin or StorageClass | Created by application/user |
| Represents actual storage | Represents storage requirement |
| Cluster resource | Namespace resource |

---

# 📝 Key Takeaways

- PVCs request storage from Kubernetes.
- PVCs bind to suitable Persistent Volumes.
- Pods should use PVCs instead of directly referencing PVs.
- Storage Classes simplify storage provisioning.
- PVCs make applications portable and easier to manage.

---

# 📋 Summary

In this chapter, you learned:

- Persistent Volume Claims
- PVC Components
- Access Modes
- Storage Classes
- YAML Examples
- Commands
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is a PVC?
2. Why do Pods use PVCs?
3. What is the purpose of a PV?
4. How do you create a PVC?
5. How do you list PVCs?

---

## Intermediate

6. Explain PVC architecture.
7. Difference between PV and PVC?
8. What are Access Modes?
9. What is a StorageClass?
10. How does a PVC bind to a PV?

---

## Advanced

11. Explain dynamic provisioning.
12. What happens if no matching PV exists?
13. How would you design storage for a database application?
14. Why should applications use PVCs instead of PVs?
15. Explain ReadWriteMany and when it is used.

---

# 🎯 Practice Exercises

## Exercise 1

Create a PVC.

---

## Exercise 2

Verify the PVC.

```bash
kubectl get pvc
```

---

## Exercise 3

Mount the PVC inside a Pod.

---

## Exercise 4

Describe the PVC.

```bash
kubectl describe pvc app-pvc
```

---

## Exercise 5

Delete the PVC.

```bash
kubectl delete pvc app-pvc
```

---

# 🧩 Mini Project

Create a Markdown file named:

```text
kubernetes-pvc-guide.md
```

Include:

- PVC Overview
- YAML Example
- Access Modes
- Storage Classes
- Commands
- Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add Kubernetes PVC guide"
```

---

# 📚 Further Reading

- Kubernetes Persistent Volume Claims Documentation
- Kubernetes Storage Classes
- Kubernetes Storage Concepts
- Kubernetes API Reference

---

# 📚 Navigation

| ⬅️ Previous | 🏠 Home | ➡️ Next |
|------------|---------|---------|
| [15 - Volumes and Persistent Volumes](15-Volumes-and-PersistentVolumes.md) | [Kubernetes Roadmap](README.md) | [17 - StorageClasses.md](17-StorageClasses.md) |

---

# 🚀 What's Next?

In **Chapter 17 – StorageClasses**, you'll learn:

- 💾 What are StorageClasses?
- ⚙️ Dynamic Provisioning
- 📦 Default StorageClass
- 📝 StorageClass YAML
- 🔄 Volume Binding
- 💻 Storage Commands
- 🛠️ Best Practices
