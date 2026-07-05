# Kubernetes Notes
# Chapter 23 - Probes (Liveness, Readiness & Startup)

> 📘 **Level:** Beginner to Intermediate
> ⏱️ **Estimated Reading Time:** 60–75 minutes
> 🛠️ **Practice Time:** 3–4 hours

---

# 📚 Table of Contents

1. What are Probes?
2. Why Use Probes?
3. Types of Probes
4. Probe Architecture
5. Liveness Probe
6. Readiness Probe
7. Startup Probe
8. Probe YAML
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

- Understand Kubernetes Probes
- Configure Liveness, Readiness, and Startup Probes
- Improve application availability
- Detect unhealthy containers
- Manage application health checks

---

# 📖 What are Probes?

A **Probe** is a health check performed by Kubernetes to determine the status of a container.

Kubernetes periodically checks your application and decides whether it should:

- Continue running
- Receive traffic
- Be restarted

Probes improve application reliability and availability.

---

# 💡 Why Use Probes?

Without Probes:

```text
Application Hangs

↓

Kubernetes Doesn't Know

↓

Users Receive Errors ❌
```

With Probes:

```text
Application Hangs

↓

Probe Detects Failure

↓

Container Restarted

↓

Application Recovers ✅
```

Benefits:

- ✅ Automatic recovery
- ✅ Better availability
- ✅ Prevents sending traffic to unhealthy Pods
- ✅ Improves production reliability

---

# 🔄 Types of Probes

| Probe | Purpose |
|--------|---------|
| Liveness Probe | Checks if the container is alive |
| Readiness Probe | Checks if the application is ready to receive traffic |
| Startup Probe | Checks whether the application has finished starting |

---

# 🏗️ Probe Architecture

```text
          Kubernetes

               │

               ▼

            Probe

               │

     ┌─────────┼─────────┐
     ▼         ▼         ▼

 Liveness  Readiness  Startup

               │

               ▼

            Container
```

---

# ❤️ Liveness Probe

The **Liveness Probe** determines whether the application is still running properly.

If it fails repeatedly, Kubernetes restarts the container.

Example:

```text
Application Frozen

↓

Liveness Probe Fails

↓

Container Restarted
```

---

# 🚦 Readiness Probe

The **Readiness Probe** determines whether the application is ready to accept requests.

If it fails:

- The Pod is **not restarted**
- The Pod is temporarily removed from the Service endpoints

Example:

```text
Application Starting

↓

Readiness Fails

↓

No Traffic Sent

↓

Ready

↓

Traffic Allowed
```

---

# 🚀 Startup Probe

The **Startup Probe** checks whether a slow-starting application has completed initialization.

Useful for:

- Java applications
- Spring Boot
- Large enterprise applications

It prevents Kubernetes from restarting applications before they finish starting.

---

# 📝 Probe YAML

```yaml
apiVersion: v1
kind: Pod

metadata:
  name: nginx-pod

spec:
  containers:
    - name: nginx
      image: nginx

      livenessProbe:
        httpGet:
          path: /
          port: 80

      readinessProbe:
        httpGet:
          path: /
          port: 80

      startupProbe:
        httpGet:
          path: /
          port: 80
```

Create the Pod:

```bash
kubectl apply -f pod.yaml
```

---

# ⚙️ Common Probe Options

| Option | Description |
|---------|-------------|
| initialDelaySeconds | Wait before first check |
| periodSeconds | Time between checks |
| timeoutSeconds | Probe timeout |
| successThreshold | Successful checks required |
| failureThreshold | Failed checks before action |

---

# 💻 Useful Commands

Create Pod:

```bash
kubectl apply -f pod.yaml
```

View Pods:

```bash
kubectl get pods
```

Describe Pod:

```bash
kubectl describe pod nginx-pod
```

View Events:

```bash
kubectl get events
```

Delete Pod:

```bash
kubectl delete pod nginx-pod
```

---

# 🏗️ Probe Workflow

```text
Pod Running

↓

Probe Executes

↓

Application Healthy?

↓

Yes → Continue Running

No → Restart or Remove from Service
```

---

# 🏆 Best Practices

- ✅ Configure both Liveness and Readiness Probes.
- ✅ Use Startup Probes for slow-starting applications.
- ✅ Avoid aggressive probe intervals.
- ✅ Test probe configurations before production.
- ✅ Monitor probe failures using logs and events.
- ✅ Use lightweight health check endpoints.

---

# 🌍 Common Use Cases

| Scenario | Liveness | Readiness | Startup |
|----------|----------|-----------|----------|
| Web Application | ✅ | ✅ | ❌ |
| REST API | ✅ | ✅ | ❌ |
| Spring Boot App | ✅ | ✅ | ✅ |
| Java Application | ✅ | ✅ | ✅ |
| Database Proxy | ✅ | ✅ | ✅ |

---

# 🔄 Liveness vs Readiness vs Startup

| Feature | Liveness | Readiness | Startup |
|---------|----------|-----------|----------|
| Detects application crash | ✅ | ❌ | ❌ |
| Controls traffic | ❌ | ✅ | ❌ |
| Restarts container | ✅ | ❌ | ❌ |
| Handles slow startup | ❌ | ❌ | ✅ |

---

# 📝 Key Takeaways

- Probes improve application health monitoring.
- Liveness restarts unhealthy containers.
- Readiness controls when traffic reaches Pods.
- Startup Probes protect slow-starting applications.
- Proper probe configuration increases application reliability.

---

# 📋 Summary

In this chapter, you learned:

- Kubernetes Probes
- Liveness Probe
- Readiness Probe
- Startup Probe
- YAML Example
- Commands
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is a Kubernetes Probe?
2. What is a Liveness Probe?
3. What is a Readiness Probe?
4. What is a Startup Probe?
5. Why are Probes important?

---

## Intermediate

6. Difference between Liveness and Readiness?
7. When should Startup Probes be used?
8. What happens when a Readiness Probe fails?
9. What happens when a Liveness Probe fails?
10. Explain probe configuration options.

---

## Advanced

11. How do Probes improve application availability?
12. Why shouldn't Liveness Probes be used for slow-starting applications?
13. How would you configure Probes for a Spring Boot application?
14. What are common mistakes when configuring Probes?
15. How do Services interact with Readiness Probes?

---

# 🎯 Practice Exercises

## Exercise 1

Create a Pod with a Liveness Probe.

---

## Exercise 2

Add a Readiness Probe.

---

## Exercise 3

Add a Startup Probe.

---

## Exercise 4

Describe the Pod.

```bash
kubectl describe pod nginx-pod
```

---

## Exercise 5

Check Pod events.

```bash
kubectl get events
```

---

# 🧩 Mini Project

Create a Markdown file named:

```text
kubernetes-probes-guide.md
```

Include:

- Probe Overview
- Liveness Probe
- Readiness Probe
- Startup Probe
- YAML Example
- Commands
- Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add Kubernetes Probes guide"
```

---

# 📚 Further Reading

- Kubernetes Probes Documentation
- Kubernetes Pod Lifecycle
- Kubernetes Health Checks
- Kubernetes API Reference

---

# 📚 Navigation

| ⬅️ Previous | 🏠 Home | ➡️ Next |
|------------|---------|---------|
| [22 - Resource Requests and Limits](22-Resource-Requests-and-Limits.md) | [Kubernetes Roadmap](README.md) | [24 - Horizontal Pod Autoscaler](24-Horizontal-Pod-Autoscaler.md) |

---

# 🚀 What's Next?

In **Chapter 24 – Horizontal Pod Autoscaler (HPA)**, you'll learn:

- 📈 What is HPA?
- ⚖️ Automatic Pod Scaling
- 📊 Metrics Server
- 📝 HPA YAML
- 💻 HPA Commands
- 🛠️ Best Practices
