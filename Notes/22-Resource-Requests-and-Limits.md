# Kubernetes Notes
# Chapter 22 - Resource Requests and Limits

> 📘 **Level:** Beginner to Intermediate
> ⏱️ **Estimated Reading Time:** 60–75 minutes
> 🛠️ **Practice Time:** 3–4 hours

---

# 📚 Table of Contents

1. What are Resource Requests and Limits?
2. Why Use Resource Management?
3. Requests vs Limits
4. Resource Architecture
5. Resource YAML
6. CPU and Memory Units
7. Managing Resources
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

- Understand CPU and Memory Requests
- Configure Resource Limits
- Prevent resource overuse
- Improve cluster stability
- Manage application resources effectively

---

# 📖 What are Resource Requests and Limits?

Kubernetes allows you to define how much **CPU** and **Memory** a container needs.

Two values can be configured:

- **Requests** – Minimum resources guaranteed to a container.
- **Limits** – Maximum resources a container is allowed to use.

This helps Kubernetes schedule Pods efficiently.

---

# 💡 Why Use Resource Management?

Without Requests & Limits:

```text
Pod

↓

Uses Unlimited CPU & Memory

↓

Other Pods Affected ❌
```

With Requests & Limits:

```text
Pod

↓

Guaranteed Resources

↓

Maximum Usage Controlled

↓

Stable Cluster ✅
```

Benefits:

- ✅ Prevent resource starvation
- ✅ Better scheduling
- ✅ Fair resource sharing
- ✅ Improved cluster performance

---

# 🔄 Requests vs Limits

| Resource | Request | Limit |
|----------|---------|-------|
| CPU | Minimum guaranteed | Maximum allowed |
| Memory | Minimum guaranteed | Maximum allowed |

Example:

```text
CPU Request : 250m

CPU Limit   : 500m

Memory Request : 256Mi

Memory Limit   : 512Mi
```

---

# 🏗️ Resource Architecture

```text
           Pod

            │

     Resource Requests

            │

     Kubernetes Scheduler

            │

      Node Selected

            │

      Resource Limits

            │

      Container Running
```

---

# 📝 Resource YAML

```yaml
apiVersion: v1
kind: Pod

metadata:
  name: nginx-pod

spec:
  containers:
    - name: nginx
      image: nginx

      resources:
        requests:
          cpu: "250m"
          memory: "256Mi"

        limits:
          cpu: "500m"
          memory: "512Mi"
```

Create the Pod:

```bash
kubectl apply -f pod.yaml
```

---

# 💾 CPU and Memory Units

### CPU

| Value | Meaning |
|-------|----------|
| 1000m | 1 CPU Core |
| 500m | 0.5 CPU |
| 250m | 0.25 CPU |

---

### Memory

| Value | Meaning |
|-------|----------|
| Mi | Mebibytes |
| Gi | Gibibytes |

Examples:

```text
256Mi

512Mi

1Gi

2Gi
```

---

# ⚙️ Managing Resources

View Pod details:

```bash
kubectl describe pod nginx-pod
```

View resource usage (Metrics Server required):

```bash
kubectl top pod
```

View node usage:

```bash
kubectl top node
```

---

# 💻 Useful Commands

Create Pod:

```bash
kubectl apply -f pod.yaml
```

Describe Pod:

```bash
kubectl describe pod nginx-pod
```

View Pod Usage:

```bash
kubectl top pod
```

View Node Usage:

```bash
kubectl top node
```

Delete Pod:

```bash
kubectl delete pod nginx-pod
```

---

# 🏗️ Resource Workflow

```text
Pod Created

↓

Scheduler Reads Requests

↓

Node Selected

↓

Container Starts

↓

Limits Enforced
```

---

# 🏆 Best Practices

- ✅ Always define Requests and Limits.
- ✅ Start with realistic values.
- ✅ Monitor CPU and Memory usage.
- ✅ Avoid setting limits too low.
- ✅ Use Horizontal Pod Autoscaler (HPA) when needed.
- ✅ Review resource settings regularly.

---

# 🌍 Common Use Cases

| Scenario | Requests & Limits |
|----------|-------------------|
| Web Application | ✅ |
| API Server | ✅ |
| Database | ✅ |
| Batch Processing | ✅ |
| Microservices | ✅ |

---

# 🔄 Requests vs Limits

| Requests | Limits |
|----------|---------|
| Used for scheduling | Used for runtime enforcement |
| Guaranteed resources | Maximum resources |
| Helps scheduler choose a node | Prevents excessive usage |
| Recommended | Recommended |

---

# 📝 Key Takeaways

- Requests define guaranteed resources.
- Limits define maximum allowed resources.
- Proper resource settings improve cluster stability.
- CPU is measured in millicores (m).
- Memory is measured in Mi and Gi.

---

# 📋 Summary

In this chapter, you learned:

- Resource Requests
- Resource Limits
- CPU & Memory Units
- YAML Example
- Commands
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is a resource request?
2. What is a resource limit?
3. Why do we configure CPU and memory?
4. What does 500m CPU mean?
5. How do you view Pod resource usage?

---

## Intermediate

6. Difference between Requests and Limits?
7. What happens if a Pod exceeds its memory limit?
8. How does the scheduler use Requests?
9. What are CPU millicores?
10. Why are Requests important?

---

## Advanced

11. Explain Kubernetes resource scheduling.
12. How do Requests and Limits improve cluster stability?
13. What happens when a container exceeds its CPU limit?
14. How would you determine appropriate resource values?
15. Explain the relationship between Requests, Limits, and HPA.

---

# 🎯 Practice Exercises

## Exercise 1

Create a Pod with Requests and Limits.

---

## Exercise 2

Describe the Pod.

```bash
kubectl describe pod nginx-pod
```

---

## Exercise 3

Monitor Pod resource usage.

```bash
kubectl top pod
```

---

## Exercise 4

Monitor Node resource usage.

```bash
kubectl top node
```

---

## Exercise 5

Delete the Pod.

```bash
kubectl delete pod nginx-pod
```

---

# 🧩 Mini Project

Create a Markdown file named:

```text
kubernetes-resource-management-guide.md
```

Include:

- Resource Requests
- Resource Limits
- CPU & Memory Units
- YAML Example
- Commands
- Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add Kubernetes Resource Management guide"
```

---

# 📚 Further Reading

- Kubernetes Resource Management Documentation
- Kubernetes Scheduler
- Metrics Server Documentation
- Kubernetes API Reference

---

# 📚 Navigation

| ⬅️ Previous | 🏠 Home | ➡️ Next |
|------------|---------|---------|
| [21 - Node Selectors and Affinity](21-Node-Selectors-and-Affinity.md) | [Kubernetes Roadmap](README.md) | [23 - Horizontal Pod Autoscaler.md](23-Horizontal-Pod-Autoscaler.md) |

---

# 🚀 What's Next?

In **Chapter 23 – Horizontal Pod Autoscaler (HPA)**, you'll learn:

- 📈 What is HPA?
- ⚖️ Auto Scaling Pods
- 📊 Metrics Server
- 📝 HPA YAML
- 💻 HPA Commands
- 🛠️ Best Practices
