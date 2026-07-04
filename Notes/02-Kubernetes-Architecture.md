# Kubernetes Notes
# Chapter 02 - Kubernetes Architecture

> 📘 **Level:** Beginner
> ⏱️ **Estimated Reading Time:** 60–75 minutes
> 🛠️ **Practice Time:** 3–4 hours

---

# 📚 Table of Contents

1. What is Kubernetes Architecture?
2. Kubernetes Cluster
3. Control Plane
4. Worker Nodes
5. API Server
6. etcd
7. Scheduler
8. Controller Manager
9. Kubelet
10. Kube Proxy
11. Container Runtime
12. Architecture Workflow
13. Summary
14. Interview Questions
15. Practice Exercises
16. Mini Project
17. Further Reading

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Understand Kubernetes architecture
- Learn the role of the Control Plane
- Understand Worker Nodes
- Learn how Kubernetes components communicate
- Understand the lifecycle of application deployment

---

# 📖 What is Kubernetes Architecture?

A Kubernetes cluster consists of one or more **Control Plane** nodes and one or more **Worker Nodes**.

The Control Plane manages the cluster, while Worker Nodes run your applications.

---

# 🏗️ Kubernetes Cluster

A Kubernetes Cluster is a group of machines working together to run containerized applications.

```text
              Kubernetes Cluster
        ┌────────────────────────────┐
        │                            │
        │      Control Plane         │
        │                            │
        └─────────────┬──────────────┘
                      │
      ┌───────────────┼───────────────┐
      ▼               ▼               ▼
 Worker Node 1   Worker Node 2   Worker Node 3
```

---

# 🧠 Control Plane

The **Control Plane** is the brain of Kubernetes.

Responsibilities:

- Manage the cluster
- Schedule Pods
- Monitor cluster health
- Maintain desired state
- Handle API requests

Main Components:

- API Server
- etcd
- Scheduler
- Controller Manager

---

# 🖥️ Worker Nodes

Worker Nodes are machines where containers actually run.

Each Worker Node contains:

- Kubelet
- Kube Proxy
- Container Runtime
- Pods

```text
Worker Node

↓

Kubelet

↓

Container Runtime

↓

Pods
```

---

# 🌐 API Server

The **API Server** is the entry point to the Kubernetes cluster.

Responsibilities:

- Accepts API requests
- Validates requests
- Updates cluster state
- Communicates with other components

Every Kubernetes operation passes through the API Server.

---

# 🗄️ etcd

**etcd** is Kubernetes' distributed key-value database.

It stores:

- Cluster configuration
- Node information
- Pod information
- Secrets
- ConfigMaps
- Current cluster state

Think of etcd as the **database of Kubernetes**.

---

# 📅 Scheduler

The Scheduler decides **which Worker Node should run a Pod**.

It considers:

- Available CPU
- Available Memory
- Node Health
- Taints & Tolerations
- Affinity Rules

```text
New Pod

↓

Scheduler

↓

Best Worker Node
```

---

# 🔄 Controller Manager

The Controller Manager continuously checks whether the cluster matches the desired state.

Examples:

- Restart failed Pods
- Create missing Pods
- Remove extra Pods
- Replace unhealthy nodes

Example:

Desired Pods:

```text
3 Pods
```

Running Pods:

```text
2 Pods
```

Controller Manager automatically creates the missing Pod.

---

# ⚙️ Kubelet

Kubelet runs on every Worker Node.

Responsibilities:

- Receives instructions from API Server
- Starts containers
- Stops containers
- Reports node health
- Monitors Pods

Without Kubelet, Pods cannot run.

---

# 🌐 Kube Proxy

Kube Proxy manages networking for Pods.

Responsibilities:

- Network routing
- Service discovery
- Load balancing
- Pod communication

It ensures network traffic reaches the correct Pod.

---

# 📦 Container Runtime

The Container Runtime is responsible for running containers.

Examples:

- containerd
- CRI-O

Responsibilities:

- Pull images
- Start containers
- Stop containers
- Manage container lifecycle

---

# 🔄 Kubernetes Deployment Workflow

```text
Developer

↓

kubectl Apply

↓

API Server

↓

etcd

↓

Scheduler

↓

Worker Node

↓

Kubelet

↓

Container Runtime

↓

Pod Running
```

---

# 🏛️ Complete Kubernetes Architecture

```text
                  User
                    │
                    ▼
                kubectl
                    │
                    ▼
              API Server
                    │
        ┌───────────┼───────────┐
        ▼           ▼           ▼
      etcd     Scheduler   Controller
                                │
        ─────────────────────────────
                    │
         Worker Node 1      Worker Node 2
         ┌───────────┐      ┌───────────┐
         │ Kubelet   │      │ Kubelet   │
         │ KubeProxy │      │ KubeProxy │
         │ Runtime   │      │ Runtime   │
         │ Pods      │      │ Pods      │
         └───────────┘      └───────────┘
```

---

# 📊 Component Summary

| Component | Purpose |
|-----------|---------|
| Control Plane | Manages cluster |
| API Server | Entry point |
| etcd | Stores cluster data |
| Scheduler | Assigns Pods to nodes |
| Controller Manager | Maintains desired state |
| Worker Node | Runs applications |
| Kubelet | Manages Pods |
| Kube Proxy | Handles networking |
| Container Runtime | Runs containers |

---

# 📝 Key Takeaways

- A Kubernetes cluster consists of Control Plane and Worker Nodes.
- The API Server is the central communication point.
- etcd stores cluster information.
- Scheduler selects the best node for Pods.
- Controller Manager maintains the desired state.
- Kubelet manages Pods on Worker Nodes.
- Kube Proxy enables networking between Pods.

---

# 📋 Summary

In this chapter, you learned:

- Kubernetes Architecture
- Cluster Components
- Control Plane
- Worker Nodes
- API Server
- etcd
- Scheduler
- Controller Manager
- Kubelet
- Kube Proxy

---

# ❓ Interview Questions

## Beginner

1. What is a Kubernetes Cluster?
2. What is the Control Plane?
3. What is a Worker Node?
4. What is the API Server?
5. What is etcd?

---

## Intermediate

6. Explain the Scheduler.
7. What does Kubelet do?
8. Explain the Controller Manager.
9. What is the role of Kube Proxy?
10. What is a Container Runtime?

---

## Advanced

11. Explain the complete Kubernetes architecture.
12. How does Kubernetes schedule Pods?
13. What happens when a Pod fails?
14. How does etcd help Kubernetes?
15. Explain communication between Control Plane and Worker Nodes.

---

# 🎯 Practice Exercises

## Exercise 1

Draw the Kubernetes architecture diagram.

---

## Exercise 2

Identify all Control Plane components.

---

## Exercise 3

List Worker Node components.

---

## Exercise 4

Explain the deployment workflow in your own words.

---

## Exercise 5

Research how the Scheduler selects a Worker Node.

---

# 🧩 Mini Project

Create a Markdown file named:

```text
kubernetes-architecture.md
```

Include:

- Kubernetes Cluster
- Control Plane
- Worker Nodes
- API Server
- etcd
- Scheduler
- Controller Manager
- Kubelet
- Kube Proxy

Commit it to Git:

```bash
git add .
git commit -m "Add Kubernetes Architecture notes"
```

---

# 📚 Further Reading

- Kubernetes Architecture Documentation
- Kubernetes Components
- Kubernetes Cluster Administration
- Kubernetes Concepts

---

# 📚 Navigation

| ⬅️ Previous | 🏠 Home | ➡️ Next |
|------------|---------|---------|
| [01 - Introduction to Kubernetes](01-Introduction-to-Kubernetes.md) | [Kubernetes Roadmap](README.md) | [03 - Installing Kubernetes](03-Installing-Kubernetes.md) |

---

# 🚀 What's Next?

In **Chapter 03 – Installing Kubernetes**, you'll learn:

- 💻 Installation Methods
- 🛠️ Minikube
- ☸️ Kind (Kubernetes in Docker)
- ⚙️ kubeadm
- 🌐 Managed Kubernetes Services
- 📥 Installing kubectl
- 🚀 Creating Your First Cluster
