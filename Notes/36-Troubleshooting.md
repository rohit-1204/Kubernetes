# Kubernetes Notes
# Chapter 36 - Troubleshooting

> 📘 **Level:** Intermediate to Advanced
> ⏱️ **Estimated Reading Time:** 90–120 minutes
> 🛠️ **Practice Time:** 5–6 hours

---

# 📚 Table of Contents

1. What is Kubernetes Troubleshooting?
2. Troubleshooting Methodology
3. Common Kubernetes Issues
4. Pod Troubleshooting
5. Deployment Troubleshooting
6. Service Troubleshooting
7. Node Troubleshooting
8. Cluster Troubleshooting
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

- Troubleshoot Kubernetes workloads
- Diagnose Pod failures
- Debug Deployments and Services
- Investigate Node issues
- Follow a structured troubleshooting process

---

# 📖 What is Kubernetes Troubleshooting?

Kubernetes troubleshooting is the process of identifying, diagnosing, and resolving issues affecting applications, Pods, nodes, or the cluster.

A systematic approach helps reduce downtime and quickly restore services.

---

# 💡 Troubleshooting Methodology

Follow this sequence:

```text
Problem Reported

↓

Collect Information

↓

Identify Root Cause

↓

Fix the Issue

↓

Verify Solution

↓

Monitor
```

Always troubleshoot from the **outside in**:

1. Application
2. Pod
3. Service
4. Deployment
5. Node
6. Cluster

---

# 🚨 Common Kubernetes Issues

| Issue | Possible Cause |
|--------|----------------|
| Pod CrashLoopBackOff | Application crash |
| ImagePullBackOff | Invalid image or registry issue |
| Pending Pods | Insufficient resources |
| Service Not Reachable | Selector mismatch |
| Failed Scheduling | Resource constraints |
| OOMKilled | Memory limit exceeded |
| Node NotReady | Node or kubelet issue |

---

# 🐳 Pod Troubleshooting

List Pods:

```bash
kubectl get pods
```

Describe a Pod:

```bash
kubectl describe pod nginx-pod
```

View logs:

```bash
kubectl logs nginx-pod
```

View previous logs:

```bash
kubectl logs --previous nginx-pod
```

Execute inside a Pod:

```bash
kubectl exec -it nginx-pod -- /bin/bash
```

---

# 🚀 Deployment Troubleshooting

View Deployments:

```bash
kubectl get deployments
```

Describe Deployment:

```bash
kubectl describe deployment nginx-deployment
```

Check rollout status:

```bash
kubectl rollout status deployment/nginx-deployment
```

View rollout history:

```bash
kubectl rollout history deployment/nginx-deployment
```

Rollback if required:

```bash
kubectl rollout undo deployment/nginx-deployment
```

---

# 🌐 Service Troubleshooting

List Services:

```bash
kubectl get svc
```

Describe Service:

```bash
kubectl describe svc nginx-service
```

Verify Endpoints:

```bash
kubectl get endpoints
```

Common checks:

- Service selector matches Pod labels
- Target port is correct
- Pods are running
- Application is listening on the expected port

---

# 🖥️ Node Troubleshooting

List Nodes:

```bash
kubectl get nodes
```

Describe Node:

```bash
kubectl describe node worker-node
```

View resource usage:

```bash
kubectl top node
```

Check Node events:

```bash
kubectl get events --sort-by=.metadata.creationTimestamp
```

---

# ☸️ Cluster Troubleshooting

Useful commands:

View cluster information:

```bash
kubectl cluster-info
```

View all resources:

```bash
kubectl get all
```

View namespaces:

```bash
kubectl get namespaces
```

Check component health (older clusters):

```bash
kubectl get componentstatuses
```

---

# 🔍 Common Pod Statuses

| Status | Meaning |
|--------|---------|
| Running | Pod is healthy |
| Pending | Waiting to be scheduled |
| CrashLoopBackOff | Container repeatedly crashes |
| ImagePullBackOff | Image cannot be downloaded |
| Completed | Job finished successfully |
| Error | Container terminated unexpectedly |

---

# 💻 Essential Troubleshooting Commands

View Events:

```bash
kubectl get events
```

Describe Resource:

```bash
kubectl describe pod <pod-name>
```

Logs:

```bash
kubectl logs <pod-name>
```

Follow Logs:

```bash
kubectl logs -f <pod-name>
```

Resource Usage:

```bash
kubectl top pod
```

View YAML:

```bash
kubectl get pod nginx-pod -o yaml
```

---

# 🏗️ Troubleshooting Workflow

```text
User Reports Issue

↓

Check Pods

↓

Check Logs

↓

Check Events

↓

Check Services

↓

Check Deployments

↓

Check Nodes

↓

Resolve Issue
```

---

# 🚨 Common Error Messages

| Error | Solution |
|--------|----------|
| CrashLoopBackOff | Check logs and application startup |
| ImagePullBackOff | Verify image name and registry credentials |
| Pending | Check node resources and scheduling |
| OOMKilled | Increase memory limit or optimize application |
| FailedScheduling | Add resources or adjust node selectors |
| Connection Refused | Verify Service, ports, and application |

---

# 🏆 Best Practices

- ✅ Always check Events first.
- ✅ Read Pod logs before restarting Pods.
- ✅ Use `kubectl describe` frequently.
- ✅ Monitor resource utilization.
- ✅ Use Liveness and Readiness Probes.
- ✅ Keep Deployments versioned.
- ✅ Enable centralized logging.
- ✅ Monitor cluster health continuously.

---

# 🌍 Common Troubleshooting Areas

| Component | Tool |
|-----------|------|
| Pods | `kubectl logs` |
| Deployments | `kubectl rollout` |
| Services | `kubectl describe svc` |
| Nodes | `kubectl describe node` |
| Metrics | `kubectl top` |
| Events | `kubectl get events` |

---

# 📝 Key Takeaways

- Troubleshoot systematically.
- Events and logs provide the most useful information.
- Verify Pods before investigating Services.
- Check Deployments and Nodes for infrastructure issues.
- Monitoring and logging reduce troubleshooting time.

---

# 📋 Summary

In this chapter, you learned:

- Kubernetes troubleshooting methodology
- Pod troubleshooting
- Deployment troubleshooting
- Service troubleshooting
- Node troubleshooting
- Essential troubleshooting commands
- Best practices

---

# ❓ Interview Questions

## Beginner

1. What is CrashLoopBackOff?
2. How do you view Pod logs?
3. What does `kubectl describe` show?
4. Why would a Pod remain in Pending state?
5. How do you list cluster events?

---

## Intermediate

6. Explain the troubleshooting workflow.
7. How do you troubleshoot a Service?
8. Difference between `kubectl logs` and `kubectl describe`?
9. How do you troubleshoot Deployment failures?
10. What causes ImagePullBackOff?

---

## Advanced

11. How would you troubleshoot a production outage?
12. Explain OOMKilled.
13. How do you investigate Node failures?
14. Design a Kubernetes troubleshooting strategy.
15. What monitoring tools would you use alongside kubectl?

---

# 🎯 Practice Exercises

## Exercise 1

View all Pods.

```bash
kubectl get pods
```

---

## Exercise 2

Describe a failing Pod.

```bash
kubectl describe pod nginx-pod
```

---

## Exercise 3

View application logs.

```bash
kubectl logs nginx-pod
```

---

## Exercise 4

Check cluster events.

```bash
kubectl get events
```

---

## Exercise 5

Rollback a Deployment.

```bash
kubectl rollout undo deployment/nginx-deployment
```

---

# 🧩 Mini Project

Create a Markdown file named:

```text
kubernetes-troubleshooting-guide.md
```

Include:

- Troubleshooting Workflow
- Common Errors
- Essential Commands
- Pod Debugging
- Deployment Debugging
- Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add Kubernetes Troubleshooting guide"
```

---

# 📚 Further Reading

- Kubernetes Debugging Applications
- Kubernetes Troubleshooting Guide
- Kubernetes Logging Architecture
- Kubernetes Monitoring Documentation
- kubectl Command Reference

---

# 📚 Navigation

| ⬅️ Previous | 🏠 Home | ➡️ Next |
|------------|---------|---------|
| [35 - Kubernetes on GCP GKE](35-Kubernetes-on-GCP-GKE.md) | [Kubernetes Roadmap](README.md) | [37 - Production Best Practices](37-Production-Best-Practices.md) |

---

# 🚀 What's Next?

In **Chapter 37 – Production Best Practices**, you'll learn:

- 🏗️ Designing Production-Ready Clusters
- 🚀 High Availability
- 📊 Monitoring & Logging
- 🔐 Security Best Practices
- 💰 Cost Optimization
- ✅ Production Readiness Checklist
