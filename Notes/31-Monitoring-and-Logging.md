# Kubernetes Notes
# Chapter 31 - Monitoring and Logging

> 📘 **Level:** Beginner to Intermediate
> ⏱️ **Estimated Reading Time:** 75–90 minutes
> 🛠️ **Practice Time:** 4–5 hours

---

# 📚 Table of Contents

1. What is Monitoring?
2. What is Logging?
3. Why Monitoring and Logging?
4. Monitoring Architecture
5. Logging Architecture
6. Popular Tools
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

- Understand Monitoring and Logging
- Monitor Kubernetes cluster health
- Collect application logs
- Learn popular monitoring tools
- Troubleshoot production issues

---

# 📖 What is Monitoring?

**Monitoring** is the process of collecting metrics about the health and performance of a Kubernetes cluster.

Monitoring helps answer questions like:

- Is the cluster healthy?
- Is CPU usage high?
- Are Pods restarting?
- Are nodes running out of memory?

---

# 📖 What is Logging?

**Logging** is the process of collecting application and system logs.

Logs help identify:

- Application errors
- Container crashes
- API failures
- Security events

---

# 💡 Why Monitoring and Logging?

Without Monitoring:

```text
Application Failure

↓

No Alerts

↓

Late Detection ❌
```

With Monitoring:

```text
Metrics Collected

↓

Alert Triggered

↓

Issue Fixed Quickly ✅
```

Benefits:

- ✅ Faster troubleshooting
- ✅ Improved availability
- ✅ Better visibility
- ✅ Proactive issue detection

---

# 🏗️ Monitoring Architecture

```text
Pods

↓

Metrics Server

↓

Prometheus

↓

Grafana Dashboard

↓

Alerts
```

---

# 🏗️ Logging Architecture

```text
Pods

↓

Container Logs

↓

Fluentd / Fluent Bit

↓

Elasticsearch

↓

Kibana
```

---

# 🛠️ Popular Monitoring Tools

| Tool | Purpose |
|------|---------|
| Metrics Server | Resource metrics |
| Prometheus | Metrics collection |
| Grafana | Dashboards & visualization |
| Alertmanager | Alerts & notifications |

---

# 📋 Popular Logging Tools

| Tool | Purpose |
|------|---------|
| kubectl logs | View container logs |
| Fluent Bit | Log collection |
| Fluentd | Log forwarding |
| Elasticsearch | Log storage |
| Kibana | Log visualization |

---

# 💻 Useful Commands

View Pod logs:

```bash
kubectl logs nginx-pod
```

Follow logs:

```bash
kubectl logs -f nginx-pod
```

View previous logs:

```bash
kubectl logs --previous nginx-pod
```

View Pod metrics:

```bash
kubectl top pod
```

View Node metrics:

```bash
kubectl top node
```

Describe Pod:

```bash
kubectl describe pod nginx-pod
```

---

# 🏗️ Monitoring Workflow

```text
Application

↓

Metrics Generated

↓

Prometheus

↓

Grafana Dashboard

↓

Alerts
```

---

# 🏗️ Logging Workflow

```text
Application

↓

Container Logs

↓

Fluent Bit

↓

Elasticsearch

↓

Kibana
```

---

# 🏆 Best Practices

- ✅ Monitor CPU, memory, and storage.
- ✅ Centralize application logs.
- ✅ Configure alerts for critical events.
- ✅ Monitor Pod restarts.
- ✅ Use dashboards for visualization.
- ✅ Retain logs based on compliance requirements.

---

# 🌍 Common Use Cases

| Scenario | Monitoring | Logging |
|----------|------------|----------|
| CPU Monitoring | ✅ | ❌ |
| Memory Monitoring | ✅ | ❌ |
| Application Errors | ❌ | ✅ |
| Debugging | ❌ | ✅ |
| Performance Analysis | ✅ | ✅ |

---

# 🔄 Monitoring vs Logging

| Monitoring | Logging |
|------------|---------|
| Collects metrics | Collects log messages |
| Shows trends | Shows detailed events |
| Detects performance issues | Helps debug failures |
| Uses dashboards | Uses log viewers |

---

# 📝 Key Takeaways

- Monitoring tracks cluster health and performance.
- Logging captures application and system events.
- Prometheus and Grafana are popular monitoring tools.
- Fluent Bit and Elasticsearch are commonly used for logging.
- Together, monitoring and logging improve observability.

---

# 📋 Summary

In this chapter, you learned:

- Monitoring
- Logging
- Monitoring Architecture
- Logging Architecture
- Popular Tools
- Commands
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is monitoring?
2. What is logging?
3. Why are both important?
4. Which command shows Pod logs?
5. Which command shows Pod resource usage?

---

## Intermediate

6. Explain the Prometheus architecture.
7. What is Grafana used for?
8. Difference between monitoring and logging?
9. Why is centralized logging important?
10. Explain Metrics Server.

---

## Advanced

11. Design a monitoring stack for Kubernetes.
12. Explain the EFK logging stack.
13. How would you monitor production clusters?
14. How do alerts improve operations?
15. Explain observability in Kubernetes.

---

# 🎯 Practice Exercises

## Exercise 1

View Pod logs.

```bash
kubectl logs nginx-pod
```

---

## Exercise 2

Follow application logs.

```bash
kubectl logs -f nginx-pod
```

---

## Exercise 3

View Pod metrics.

```bash
kubectl top pod
```

---

## Exercise 4

View Node metrics.

```bash
kubectl top node
```

---

## Exercise 5

Describe a Pod.

```bash
kubectl describe pod nginx-pod
```

---

# 🧩 Mini Project

Create a Markdown file named:

```text
kubernetes-monitoring-guide.md
```

Include:

- Monitoring Overview
- Logging Overview
- Monitoring Tools
- Logging Tools
- Commands
- Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add Kubernetes Monitoring and Logging guide"
```

---

# 📚 Further Reading

- Kubernetes Monitoring Documentation
- Prometheus Documentation
- Grafana Documentation
- Fluent Bit Documentation
- Elasticsearch Documentation

---

# 📚 Navigation

| ⬅️ Previous | 🏠 Home | ➡️ Next |
|------------|---------|---------|
| [30 - Kustomize](30-Kustomize.md) | [Kubernetes Roadmap](README.md) | [32 - Security Best Practices](32-Security-Best-Practices.md) |

---

# 🚀 What's Next?

In **Chapter 32 – Security Best Practices**, you'll learn:

- 🔐 Kubernetes Security Fundamentals
- 🛡️ Pod Security
- 🔑 Secrets Management
- 🌐 Network Security
- 👤 RBAC Best Practices
- 🚀 Production Security Checklist
