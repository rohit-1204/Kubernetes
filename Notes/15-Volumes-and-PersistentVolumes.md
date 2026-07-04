# Kubernetes Notes
# Chapter 15 - Volumes and Persistent Volumes

> 📘 **Level:** Beginner
> ⏱️ **Estimated Reading Time:** 60–75 minutes
> 🛠️ **Practice Time:** 3–4 hours

---

# 📚 Table of Contents

1. What are Volumes?
2. Why Use Volumes?
3. Types of Volumes
4. What is a Persistent Volume (PV)?
5. What is a Persistent Volume Claim (PVC)?
6. Volume Architecture
7. Volume YAML
8. Persistent Volume YAML
9. Persistent Volume Claim YAML
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

- Understand Kubernetes Volumes
- Learn Persistent Volumes (PV)
- Learn Persistent Volume Claims (PVC)
- Mount storage inside Pods
- Manage persistent storage

---

# 📖 What are Volumes?

A **Volume** is a storage resource attached to a Pod.

Unlike the container filesystem, a Volume remains available even if a container inside the Pod restarts.

> **Note:** If the Pod itself is deleted, most regular volumes are also deleted unless persistent storage is used.

---

# 💡 Why Use Volumes?

Without Volumes:

```text
Container

↓

Store Data

↓

Container Restart

↓

Data Lost ❌
```

With Volumes:

```text
Container

↓

Volume

↓

Container Restart

↓

Data Preserved ✅
```

Benefits:

- ✅ Persistent application data
- ✅ Share data between containers
- ✅ Separate storage from containers
- ✅ Better application reliability

---

# 📂 Types of Volumes

Common Kubernetes volume types:

| Volume Type | Purpose |
|-------------|----------|
| emptyDir | Temporary storage for a Pod |
| hostPath | Uses a directory from the Node |
| configMap | Mounts ConfigMap data |
| secret | Mounts Secret data |
| persistentVolumeClaim | Uses Persistent Storage |

---

# 💾 What is a Persistent Volume (PV)?

A **Persistent Volume (PV)** is a storage resource managed by the Kubernetes cluster.

It exists independently of Pods and provides long-term storage.

Examples:

- AWS EBS
- Azure Disk
- Google Persistent Disk
- NFS
- Local Storage

---

# 📦 What is a Persistent Volume Claim (PVC)?

A **Persistent Volume Claim (PVC)** is a request for storage made by a Pod.

The PVC automatically binds to a matching Persistent Volume.

```text
Pod

↓

PVC

↓

PV

↓

Storage
```

---

# 🏗️ Volume Architecture

```text
              Pod
               │
         Volume Mount
               │
              PVC
               │
               PV
               │
      Physical Storage
```

---

# 📝 Volume YAML

Example using an `emptyDir` volume:

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
        - name: app-storage
          mountPath: /usr/share/nginx/html

  volumes:
    - name: app-storage
      emptyDir: {}
```

Create the Pod:

```bash
kubectl apply -f pod.yaml
```

---

# 📝 Persistent Volume YAML

```yaml
apiVersion: v1
kind: PersistentVolume

metadata:
  name: app-pv

spec:
  capacity:
    storage: 5Gi

  accessModes:
    - ReadWriteOnce

  hostPath:
    path: /data/storage
```

Create the PV:

```bash
kubectl apply -f pv.yaml
```

---

# 📝 Persistent Volume Claim YAML

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

# ⚙️ Managing Volumes

List Persistent Volumes:

```bash
kubectl get pv
```

List Persistent Volume Claims:

```bash
kubectl get pvc
```

Describe a PV:

```bash
kubectl describe pv app-pv
```

Describe a PVC:

```bash
kubectl describe pvc app-pvc
```

---

# 💻 Useful Commands

List PVs:

```bash
kubectl get pv
```

List PVCs:

```bash
kubectl get pvc
```

Describe PV:

```bash
kubectl describe pv app-pv
```

Describe PVC:

```bash
kubectl describe pvc app-pvc
```

Delete PVC:

```bash
kubectl delete pvc app-pvc
```

Delete PV:

```bash
kubectl delete pv app-pv
```

---

# 🏗️ Storage Workflow

```text
Create Persistent Volume

↓

Create Persistent Volume Claim

↓

PVC Binds to PV

↓

Pod Uses PVC

↓

Persistent Data Stored
```

---

# 🏆 Best Practices

- ✅ Use PVC instead of directly using PVs in Pods.
- ✅ Use Storage Classes for dynamic provisioning.
- ✅ Choose the correct access mode.
- ✅ Monitor storage utilization.
- ✅ Back up persistent data regularly.
- ✅ Avoid using `hostPath` in production.

---

# 🌍 Common Use Cases

| Scenario | Storage |
|----------|---------|
| Database | ✅ PV + PVC |
| File Uploads | ✅ PV + PVC |
| Logs | ✅ PV + PVC |
| Shared Configuration | ✅ Volume |
| Temporary Cache | ✅ emptyDir |

---

# 🔄 Volume vs Persistent Volume

| Volume | Persistent Volume |
|--------|-------------------|
| Pod-level storage | Cluster-level storage |
| Usually temporary | Persistent |
| Deleted with Pod (depends on type) | Independent of Pods |
| Simple storage | Production storage |

---

# 📝 Key Takeaways

- Volumes provide storage to Pods.
- Persistent Volumes offer long-term storage.
- PVCs request storage from available PVs.
- Pods should use PVCs instead of directly accessing PVs.
- Storage Classes simplify dynamic storage provisioning.

---

# 📋 Summary

In this chapter, you learned:

- Volumes
- Volume Types
- Persistent Volumes
- Persistent Volume Claims
- YAML Examples
- Commands
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is a Volume?
2. Why are Volumes used?
3. What is a Persistent Volume?
4. What is a Persistent Volume Claim?
5. How do you list PVs?

---

## Intermediate

6. Explain PV and PVC.
7. Difference between Volume and PV?
8. What are access modes?
9. Why should Pods use PVCs?
10. What is `emptyDir`?

---

## Advanced

11. Explain the PV-PVC binding process.
12. What are Storage Classes?
13. Why should `hostPath` be avoided in production?
14. How would you design persistent storage for databases?
15. Explain dynamic provisioning.

---

# 🎯 Practice Exercises

## Exercise 1

Create a Persistent Volume.

---

## Exercise 2

Create a Persistent Volume Claim.

---

## Exercise 3

Verify that the PVC is bound.

```bash
kubectl get pvc
```

---

## Exercise 4

Mount the PVC inside a Pod.

---

## Exercise 5

Delete the PVC and PV.

```bash
kubectl delete pvc app-pvc

kubectl delete pv app-pv
```

---

# 🧩 Mini Project

Create a Markdown file named:

```text
kubernetes-storage-guide.md
```

Include:

- Volume Overview
- PV
- PVC
- YAML Examples
- Commands
- Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add Kubernetes Storage guide"
```

---

# 📚 Further Reading

- Kubernetes Persistent Volumes Documentation
- Kubernetes Storage Classes
- Kubernetes Volumes
- Kubernetes API Reference

---

# 📚 Navigation

| ⬅️ Previous | 🏠 Home | ➡️ Next |
|------------|---------|---------|
| [14 - Secrets](14-Secrets.md) | [Kubernetes Roadmap](README.md) | [16 - StatefulSets.md](16-StatefulSets.md) |

---

# 🚀 What's Next?

In **Chapter 16 – StatefulSets**, you'll learn:

- 📦 What are StatefulSets?
- 🆔 Stable Pod Identity
- 💾 Persistent Storage
- 🔄 Ordered Deployment
- 📝 StatefulSet YAML
- 💻 StatefulSet Commands
- 🛠️ Best Practices
