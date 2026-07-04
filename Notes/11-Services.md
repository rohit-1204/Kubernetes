# Kubernetes Notes
# Chapter 11 - Services

> 📘 **Level:** Beginner
> ⏱️ **Estimated Reading Time:** 60–75 minutes
> 🛠️ **Practice Time:** 3–4 hours

---

# 📚 Table of Contents

1. What is a Service?
2. Why Use Services?
3. Service Architecture
4. Types of Services
5. Service YAML
6. Creating Services
7. Managing Services
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

- Understand Kubernetes Services
- Learn different Service types
- Expose applications inside and outside the cluster
- Create and manage Services
- Use kubectl commands for Services

---

# 📖 What is a Service?

A **Service** is a Kubernetes resource that provides a **stable network endpoint** for a group of Pods.

Since Pods are temporary and their IP addresses can change, a Service provides a fixed IP address and DNS name that applications can use to communicate reliably.

---

# 💡 Why Use Services?

Without a Service:

```text
Client

↓

Pod IP

↓

Pod Deleted

↓

Connection Lost ❌
```

With a Service:

```text
Client

↓

Service

↓

Pod 1

Pod 2

Pod 3

↓

Connection Always Available ✅
```

Benefits:

- ✅ Stable IP Address
- ✅ Load Balancing
- ✅ Service Discovery
- ✅ Reliable Communication
- ✅ Easy Scaling

---

# 🏗️ Service Architecture

```text
             Client
                │
                ▼
           Kubernetes Service
                │
      ┌─────────┼─────────┐
      ▼         ▼         ▼
    Pod 1     Pod 2     Pod 3
```

The Service forwards traffic to healthy Pods using label selectors.

---

# 🌐 Types of Services

## 1. ClusterIP (Default)

- Internal communication only
- Accessible within the cluster
- Default Service type

```text
Application

↓

ClusterIP

↓

Pods
```

---

## 2. NodePort

- Exposes the application on a port of every worker node.
- Accessible using:

```text
<Node-IP>:NodePort
```

Example:

```text
192.168.1.20:30080
```

---

## 3. LoadBalancer

- Creates a cloud load balancer.
- Provides an external IP.
- Commonly used in cloud environments like AWS, Azure, and GCP.

```text
Internet

↓

Load Balancer

↓

Service

↓

Pods
```

---

## 4. ExternalName

Maps a Service to an external DNS name.

Example:

```text
database.example.com
```

Used when the application needs to access external services.

---

# 📝 Service YAML

```yaml
apiVersion: v1
kind: Service

metadata:
  name: nginx-service

spec:
  selector:
    app: nginx

  ports:
    - protocol: TCP
      port: 80
      targetPort: 80

  type: ClusterIP
```

Create the Service:

```bash
kubectl apply -f service.yaml
```

---

# 🚀 Creating Services

Create a Service:

```bash
kubectl apply -f service.yaml
```

List Services:

```bash
kubectl get services
```

View detailed information:

```bash
kubectl describe service nginx-service
```

---

# ⚙️ Managing Services

Delete a Service:

```bash
kubectl delete service nginx-service
```

Expose a Deployment:

```bash
kubectl expose deployment nginx-deployment \
--type=NodePort \
--port=80
```

View endpoints:

```bash
kubectl get endpoints
```

---

# 💻 Useful Commands

List Services:

```bash
kubectl get svc
```

Describe a Service:

```bash
kubectl describe svc nginx-service
```

View Endpoints:

```bash
kubectl get endpoints
```

Create a Service:

```bash
kubectl apply -f service.yaml
```

Delete a Service:

```bash
kubectl delete svc nginx-service
```

---

# 🏗️ Service Workflow

```text
Client

↓

Service

↓

Selector

↓

Matching Pods

↓

Application Response
```

---

# 🏆 Best Practices

- ✅ Use ClusterIP for internal applications.
- ✅ Use NodePort only for testing or learning.
- ✅ Use LoadBalancer for production applications.
- ✅ Use labels and selectors consistently.
- ✅ Monitor Service endpoints.
- ✅ Store Service YAML files in Git.

---

# 🌍 Common Use Cases

| Scenario | Service Type |
|----------|--------------|
| Internal API | ClusterIP |
| Web Application | LoadBalancer |
| Development Testing | NodePort |
| External Database | ExternalName |

---

# 🔄 ClusterIP vs NodePort vs LoadBalancer

| Feature | ClusterIP | NodePort | LoadBalancer |
|---------|-----------|-----------|---------------|
| Internal Access | ✅ | ✅ | ✅ |
| External Access | ❌ | ✅ | ✅ |
| Cloud Load Balancer | ❌ | ❌ | ✅ |
| Production Ready | ✅ | Limited | ✅ |

---

# 📝 Key Takeaways

- Services provide stable networking for Pods.
- Pods communicate using Services instead of Pod IPs.
- ClusterIP is the default Service type.
- LoadBalancer is commonly used in cloud environments.
- Services use labels and selectors to find Pods.

---

# 📋 Summary

In this chapter, you learned:

- Kubernetes Services
- Service Architecture
- Service Types
- Service YAML
- Service Commands
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is a Kubernetes Service?
2. Why do Pods need Services?
3. What is ClusterIP?
4. What is NodePort?
5. How do you list Services?

---

## Intermediate

6. Explain the Service architecture.
7. Difference between ClusterIP and NodePort?
8. What is a LoadBalancer Service?
9. How does a Service find Pods?
10. What are Endpoints?

---

## Advanced

11. Explain Service discovery in Kubernetes.
12. How does kube-proxy work with Services?
13. When should ExternalName be used?
14. Why shouldn't production applications rely on NodePort?
15. How would you expose an application securely in production?

---

# 🎯 Practice Exercises

## Exercise 1

Create a ClusterIP Service.

---

## Exercise 2

Expose an Nginx Deployment.

```bash
kubectl apply -f service.yaml
```

---

## Exercise 3

List all Services.

```bash
kubectl get svc
```

---

## Exercise 4

View Service details.

```bash
kubectl describe svc nginx-service
```

---

## Exercise 5

Delete the Service.

```bash
kubectl delete svc nginx-service
```

---

# 🧩 Mini Project

Create a Markdown file named:

```text
kubernetes-services-guide.md
```

Include:

- Service Overview
- Service Types
- YAML Example
- Commands
- Service Architecture
- Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add Kubernetes Services guide"
```

---

# 📚 Further Reading

- Kubernetes Services Documentation
- Kubernetes Networking
- kube-proxy Documentation
- Kubernetes API Reference

---

# 📚 Navigation

| ⬅️ Previous | 🏠 Home | ➡️ Next |
|------------|---------|---------|
| [10 - Annotations](10-Annotations.md) | [Kubernetes Roadmap](README.md) | [12 - Ingress.md](12-Ingress.md) |

---

# 🚀 What's Next?

In **Chapter 12 – Ingress**, you'll learn:

- 🌐 What is Ingress?
- 🚪 Ingress Controller
- 📝 Ingress YAML
- 🌍 Path-Based Routing
- 🌐 Host-Based Routing
- 🔒 TLS Configuration
- 💻 Ingress Commands
- 🛠️ Best Practices
