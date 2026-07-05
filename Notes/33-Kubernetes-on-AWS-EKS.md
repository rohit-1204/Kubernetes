# Kubernetes Notes
# Chapter 33 - Kubernetes on AWS EKS

> 📘 **Level:** Intermediate
> ⏱️ **Estimated Reading Time:** 75–90 minutes
> 🛠️ **Practice Time:** 4–5 hours

---

# 📚 Table of Contents

1. What is Amazon EKS?
2. Why Use EKS?
3. EKS Architecture
4. EKS Components
5. Creating an EKS Cluster
6. Managing EKS
7. Useful Commands
8. Best Practices
9. Summary
10. Interview Questions
11. Practice Exercises
12. Mini Project
13. Further Reading

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Understand Amazon EKS
- Learn EKS architecture
- Create and manage EKS clusters
- Connect using kubectl
- Deploy applications on EKS

---

# 📖 What is Amazon EKS?

**Amazon Elastic Kubernetes Service (EKS)** is a **managed Kubernetes service** provided by AWS.

AWS manages the Kubernetes control plane, while you manage your worker nodes (or use AWS managed node groups/Fargate).

Benefits include:

- Managed Kubernetes control plane
- High availability
- Automatic updates
- AWS service integration
- Production-ready clusters

---

# 💡 Why Use EKS?

Without EKS:

```text
Install Kubernetes

↓

Manage Control Plane

↓

Maintain Cluster ❌
```

With EKS:

```text
AWS Manages

↓

Kubernetes Control Plane

↓

You Deploy Applications ✅
```

Benefits:

- ✅ Managed control plane
- ✅ Highly available
- ✅ Automatic scaling support
- ✅ Secure by default
- ✅ Easy AWS integration

---

# 🏗️ EKS Architecture

```text
               Users

                 │

                 ▼

            kubectl / AWS CLI

                 │

                 ▼

          Amazon EKS Cluster

        ┌─────────┴─────────┐
        ▼                   ▼

 Control Plane         Worker Nodes

        │                   │

        └─────────┬─────────┘
                  ▼

               Kubernetes Pods
```

---

# ⚙️ EKS Components

| Component | Purpose |
|-----------|---------|
| EKS Control Plane | Managed by AWS |
| Worker Nodes | Run applications |
| Managed Node Groups | AWS-managed worker nodes |
| Fargate | Serverless Pods |
| VPC | Networking |
| IAM | Authentication & authorization |
| kubectl | Cluster management |

---

# 🚀 Creating an EKS Cluster

Using **eksctl**:

Create a cluster:

```bash
eksctl create cluster \
--name demo-cluster \
--region us-east-1 \
--nodes 2
```

Verify the cluster:

```bash
kubectl get nodes
```

Delete the cluster:

```bash
eksctl delete cluster --name demo-cluster
```

---

# 🔄 Managing EKS

Update kubeconfig:

```bash
aws eks update-kubeconfig \
--region us-east-1 \
--name demo-cluster
```

List nodes:

```bash
kubectl get nodes
```

Deploy an application:

```bash
kubectl apply -f deployment.yaml
```

View Pods:

```bash
kubectl get pods
```

---

# 💻 Useful Commands

Create Cluster:

```bash
eksctl create cluster --name demo-cluster
```

Update kubeconfig:

```bash
aws eks update-kubeconfig \
--region us-east-1 \
--name demo-cluster
```

View Nodes:

```bash
kubectl get nodes
```

View Pods:

```bash
kubectl get pods
```

Delete Cluster:

```bash
eksctl delete cluster --name demo-cluster
```

---

# 🏗️ EKS Workflow

```text
Developer

↓

eksctl

↓

Amazon EKS

↓

Managed Control Plane

↓

Worker Nodes

↓

Pods Running
```

---

# 🏆 Best Practices

- ✅ Use Managed Node Groups.
- ✅ Enable IAM Roles for Service Accounts (IRSA).
- ✅ Store Secrets securely.
- ✅ Enable Cluster Autoscaler.
- ✅ Monitor using CloudWatch and Prometheus.
- ✅ Use multiple Availability Zones.
- ✅ Keep Kubernetes versions updated.

---

# 🌍 Common Use Cases

| Scenario | EKS |
|----------|-----|
| Microservices | ✅ |
| CI/CD Deployments | ✅ |
| Production Applications | ✅ |
| AI/ML Workloads | ✅ |
| Enterprise Applications | ✅ |

---

# 🔄 Self-Managed Kubernetes vs Amazon EKS

| Self-Managed | Amazon EKS |
|--------------|------------|
| Manage control plane | AWS manages control plane |
| Manual upgrades | Managed upgrades |
| Higher maintenance | Lower maintenance |
| Full infrastructure control | AWS-managed infrastructure |
| More operational effort | Faster deployment |

---

# 📝 Key Takeaways

- Amazon EKS is a managed Kubernetes service.
- AWS manages the control plane.
- Worker nodes run your applications.
- EKS integrates with IAM, VPC, and CloudWatch.
- EKS simplifies running production Kubernetes clusters.

---

# 📋 Summary

In this chapter, you learned:

- Amazon EKS
- EKS Architecture
- Cluster Creation
- Node Management
- Commands
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is Amazon EKS?
2. Why use EKS?
3. What is managed by AWS in EKS?
4. Which tool creates an EKS cluster?
5. How do you view cluster nodes?

---

## Intermediate

6. Explain EKS architecture.
7. What are Managed Node Groups?
8. What is Fargate in EKS?
9. How does kubectl connect to EKS?
10. Why is IAM important in EKS?

---

## Advanced

11. Explain EKS networking using VPC.
12. What is IRSA (IAM Roles for Service Accounts)?
13. How would you deploy a production application on EKS?
14. Explain EKS high availability.
15. Compare EKS with self-managed Kubernetes.

---

# 🎯 Practice Exercises

## Exercise 1

Create an EKS cluster.

```bash
eksctl create cluster --name demo-cluster
```

---

## Exercise 2

Update kubeconfig.

```bash
aws eks update-kubeconfig \
--region us-east-1 \
--name demo-cluster
```

---

## Exercise 3

Verify worker nodes.

```bash
kubectl get nodes
```

---

## Exercise 4

Deploy an application.

```bash
kubectl apply -f deployment.yaml
```

---

## Exercise 5

Delete the cluster.

```bash
eksctl delete cluster --name demo-cluster
```

---

# 🧩 Mini Project

Create a Markdown file named:

```text
kubernetes-eks-guide.md
```

Include:

- Amazon EKS Overview
- EKS Architecture
- Cluster Creation
- Commands
- Best Practices
- Production Recommendations

Commit it to Git:

```bash
git add .
git commit -m "Add Kubernetes on AWS EKS guide"
```

---

# 📚 Further Reading

- Amazon EKS Documentation
- eksctl Documentation
- Kubernetes Documentation
- AWS IAM Documentation
- AWS VPC Documentation

---

# 📚 Navigation

| ⬅️ Previous | 🏠 Home | ➡️ Next |
|------------|---------|---------|
| [32 - Security Best Practices](32-Security-Best-Practices.md) | [Kubernetes Roadmap](README.md) | [34 - Kubernetes on Azure AKS](34-Kubernetes-on-Azure-AKS.md) |

---

# 🚀 What's Next?

In **Chapter 34 – Kubernetes on Azure AKS**, you'll learn:

- ☁️ What is Azure AKS?
- 🏗️ AKS Architecture
- 🚀 Creating an AKS Cluster
- 👷 Node Pools
- 💻 AKS Commands
- 🛠️ Best Practices
