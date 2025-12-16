# Kubernetes Fundamentals

Kubernetes is not a tool you “memorize.”  
It’s a system you **understand**.

This document covers the **core fundamentals** you must master before touching advanced topics like Helm, Operators, or managed Kubernetes services.

---

## What is Kubernetes?

Kubernetes is an **open-source container orchestration platform** designed to:

- Deploy containerized applications
- Scale them automatically
- Heal failures without human intervention
- Manage networking and service discovery

🚫 Kubernetes is **not** a Docker replacement.  
✅ Docker builds containers. Kubernetes **runs and manages** them at scale.

---

## Core Kubernetes Architecture

A Kubernetes cluster has two main parts:

### 1. Control Plane (Brain of the Cluster)

Responsible for managing the cluster state.

- **API Server**
  - Entry point for all requests (`kubectl`, CI/CD, UI)
  - Validates and processes manifests

- **Scheduler**
  - Decides *which node* a Pod should run on
  - Considers CPU, memory, taints, and constraints

- **Controller Manager**
  - Continuously checks:
    > Desired state == Actual state
  - Fixes drift automatically

- **etcd**
  - Distributed key-value store
  - Single source of truth for cluster state

---

### 2. Worker Nodes (Execution Layer)

Where applications actually run.

- **Node**
  - VM or physical machine
  - Runs Pods

- **kubelet**
  - Talks to the API Server
  - Ensures containers are running as expected

- **Container Runtime**
  - containerd / CRI-O
  - Pulls images and runs containers

---

## Core Kubernetes Objects (Non-Negotiable)

### Pod
- Smallest deployable unit
- One or more containers
- Ephemeral by design

> Pods are **not** meant to be long-lived.

---

### Deployment
- Manages Pods declaratively
- Handles:
  - Rolling updates
  - Rollbacks
  - Scaling

You declare **what you want**, Kubernetes figures out **how to keep it that way**.

---

### Service
- Provides stable networking
- Abstracts Pod IP changes

Common types:
- `ClusterIP`
- `NodePort`
- `LoadBalancer`

---

## Desired State vs Actual State

This is the **core Kubernetes philosophy**.

You declare:
```yaml
replicas: 3
```
Kubernetes ensures:

3 Pods are always running

If one dies, another is created automatically


No manual intervention. No heroics.


---

Why Kubernetes Exists (The Real Reason)

Containers crash → Kubernetes restarts them

Traffic spikes → Kubernetes scales Pods

Nodes fail → Kubernetes reschedules workloads


Kubernetes removes human dependency from production systems.


---

Common Beginner Mistakes

❌ Treating Pods like VMs
❌ Hardcoding IPs
❌ Ignoring liveness/readiness probes
❌ Jumping to Helm before understanding YAML
❌ Memorizing kubectl commands without understanding architecture


---

How to Learn Kubernetes Properly

1. Understand architecture first


2. Write raw YAML manifests


3. Break things intentionally


4. Observe how Kubernetes self-heals


5. Only then move to Helm / managed services




---

Final Advice

If you don’t understand:

Declarative configuration

Desired state

Why Pods are disposable


You don’t understand Kubernetes — you’re just running commands.

Master the fundamentals. Kubernetes rewards depth, not shortcuts.


---

📌 This repository is part of my Learning in Public journey.
Feel free to fork, star, or contribute improvements.

---
