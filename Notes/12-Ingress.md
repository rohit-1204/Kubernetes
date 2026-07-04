# Kubernetes Notes
# Chapter 12 - Ingress

> 📘 **Level:** Beginner to Intermediate
> ⏱️ **Estimated Reading Time:** 60–75 minutes
> 🛠️ **Practice Time:** 3–4 hours

---

# 📚 Table of Contents

1. What is Ingress?
2. Why Use Ingress?
3. Ingress Architecture
4. Ingress Controller
5. Types of Routing
6. Ingress YAML
7. TLS with Ingress
8. Managing Ingress
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

- Understand Kubernetes Ingress
- Learn the role of an Ingress Controller
- Configure path-based and host-based routing
- Secure applications using TLS
- Create and manage Ingress resources

---

# 📖 What is Ingress?

An **Ingress** is a Kubernetes resource that manages **external HTTP and HTTPS access** to applications running inside the cluster.

Instead of exposing every application using a separate LoadBalancer, Ingress provides a **single entry point** for multiple services.

> **Note:** An Ingress resource requires an **Ingress Controller** to function.

---

# 💡 Why Use Ingress?

Without Ingress:

```text
Internet

↓

LoadBalancer (App 1)

LoadBalancer (App 2)

LoadBalancer (App 3)

↓

Higher Cost ❌
```

With Ingress:

```text
Internet

↓

Ingress Controller

↓

Ingress

↓

Service A

Service B

Service C

↓

Lower Cost ✅
```

Benefits:

- ✅ Single entry point
- ✅ Path-based routing
- ✅ Host-based routing
- ✅ SSL/TLS termination
- ✅ Lower cloud costs

---

# 🏗️ Ingress Architecture

```text
            Internet
                │
                ▼
      Ingress Controller
                │
             Ingress
      ┌─────────┼─────────┐
      ▼         ▼         ▼
  Service A  Service B  Service C
      │         │         │
     Pods      Pods      Pods
```

---

# ⚙️ Ingress Controller

An **Ingress Controller** watches Ingress resources and configures routing accordingly.

Popular Ingress Controllers:

- NGINX Ingress Controller
- AWS Load Balancer Controller
- Traefik
- HAProxy Ingress
- Kong Ingress Controller

Without an Ingress Controller, Ingress resources do nothing.

---

# 🌐 Types of Routing

## Path-Based Routing

Different URL paths route to different services.

Example:

```text
example.com/app1 → Service A

example.com/app2 → Service B
```

---

## Host-Based Routing

Different domain names route to different services.

Example:

```text
app.example.com → Service A

api.example.com → Service B
```

---

# 📝 Ingress YAML

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress

metadata:
  name: app-ingress

spec:
  rules:
    - host: app.example.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: nginx-service
                port:
                  number: 80
```

Create the Ingress:

```bash
kubectl apply -f ingress.yaml
```

---

# 🔒 TLS with Ingress

Ingress supports HTTPS using TLS certificates.

Example:

```yaml
tls:
  - hosts:
      - app.example.com
    secretName: app-tls
```

The TLS certificate is stored as a Kubernetes Secret.

Benefits:

- ✅ HTTPS
- ✅ Secure communication
- ✅ Data encryption

---

# ⚙️ Managing Ingress

List Ingress resources:

```bash
kubectl get ingress
```

Describe an Ingress:

```bash
kubectl describe ingress app-ingress
```

Delete an Ingress:

```bash
kubectl delete ingress app-ingress
```

---

# 💻 Useful Commands

Create Ingress:

```bash
kubectl apply -f ingress.yaml
```

List Ingress:

```bash
kubectl get ingress
```

Describe Ingress:

```bash
kubectl describe ingress app-ingress
```

Delete Ingress:

```bash
kubectl delete ingress app-ingress
```

View all resources:

```bash
kubectl get all
```

---

# 🏗️ Ingress Workflow

```text
Client Request

↓

Ingress Controller

↓

Ingress Rules

↓

Service

↓

Pod

↓

Application Response
```

---

# 🏆 Best Practices

- ✅ Use one Ingress for multiple applications.
- ✅ Enable HTTPS using TLS.
- ✅ Use meaningful hostnames.
- ✅ Configure health checks.
- ✅ Monitor the Ingress Controller.
- ✅ Store Ingress YAML in Git.
- ✅ Avoid exposing services directly unless necessary.

---

# 🌍 Common Use Cases

| Scenario | Ingress |
|----------|----------|
| Web Application | ✅ |
| REST API | ✅ |
| Multiple Websites | ✅ |
| HTTPS Termination | ✅ |
| Microservices | ✅ |

---

# 🔄 Ingress vs LoadBalancer

| Feature | Ingress | LoadBalancer |
|---------|----------|--------------|
| HTTP/HTTPS Routing | ✅ | ❌ |
| Path-Based Routing | ✅ | ❌ |
| Host-Based Routing | ✅ | ❌ |
| SSL/TLS Termination | ✅ | Limited |
| Single Entry Point | ✅ | ❌ |

---

# 📝 Key Takeaways

- Ingress manages external HTTP/HTTPS traffic.
- It requires an Ingress Controller.
- Supports host-based and path-based routing.
- Reduces the number of cloud load balancers.
- Supports TLS for secure communication.

---

# 📋 Summary

In this chapter, you learned:

- Ingress
- Ingress Controller
- Routing Types
- Ingress YAML
- TLS Configuration
- Management Commands
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is an Ingress?
2. Why do we use Ingress?
3. What is an Ingress Controller?
4. How do you create an Ingress?
5. Which command lists Ingress resources?

---

## Intermediate

6. Explain path-based routing.
7. Explain host-based routing.
8. Difference between Service and Ingress?
9. Why is an Ingress Controller required?
10. How does TLS work with Ingress?

---

## Advanced

11. Explain the Ingress architecture.
12. Compare Ingress and LoadBalancer Services.
13. How would you expose multiple applications using a single Ingress?
14. How does the NGINX Ingress Controller process requests?
15. What happens if an Ingress Controller is not installed?

---

# 🎯 Practice Exercises

## Exercise 1

Create an Ingress resource.

---

## Exercise 2

Configure host-based routing.

---

## Exercise 3

Configure path-based routing.

---

## Exercise 4

Enable TLS using a Secret.

---

## Exercise 5

Verify the Ingress.

```bash
kubectl get ingress
```

---

# 🧩 Mini Project

Create a Markdown file named:

```text
kubernetes-ingress-guide.md
```

Include:

- Ingress Overview
- Ingress Controller
- Routing Types
- YAML Example
- TLS Configuration
- Commands
- Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add Kubernetes Ingress guide"
```

---

# 📚 Further Reading

- Kubernetes Ingress Documentation
- NGINX Ingress Controller
- Kubernetes Networking
- Kubernetes API Reference

---

# 📚 Navigation

| ⬅️ Previous | 🏠 Home | ➡️ Next |
|------------|---------|---------|
| [11 - Services](11-Services.md) | [Kubernetes Roadmap](README.md) | [13 - ConfigMaps.md](13-ConfigMaps.md) |

---

# 🚀 What's Next?

In **Chapter 13 – ConfigMaps**, you'll learn:

- ⚙️ What are ConfigMaps?
- 📝 Creating ConfigMaps
- 🔄 Using ConfigMaps
- 🌍 Environment Variables
- 📂 Mounting ConfigMaps as Volumes
- 💻 ConfigMap Commands
- 🛠️ Best Practices
