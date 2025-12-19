# Kubernetes Architecture Components

Understanding Kubernetes architecture is **non-negotiable** if you want to operate clusters confidently, debug production issues, or clear serious DevOps interviews.

This document breaks down Kubernetes architecture into **what actually matters**.

---

## High-Level Architecture

Kubernetes follows a **master–worker (control plane–node)** architecture:

- **Control Plane** → Decides *what should happen*
- **Worker Nodes** → Execute *what is decided*

User → kubectl / CI/CD ↓ API Server ↓ etcd ↓ Scheduler & Controllers ↓ Worker Nodes

---

## Control Plane Components (The Brain)

The control plane manages the **desired state** of the cluster.

### 1. API Server
- Central communication hub
- Validates and processes all REST requests
- Handles authentication, authorization, and admission control
- **Only component that talks to etcd**

> If the API Server is down, the cluster is effectively unusable.

---

### 2. etcd
- Distributed key-value store
- Stores **entire cluster state**
- Strongly consistent (Raft consensus)

**Stores:**
- Pod definitions
- ConfigMaps & Secrets
- Node status
- Cluster metadata

> etcd failure = data loss risk. Always back it up.

---

### 3. Scheduler
- Assigns Pods to nodes
- Considers:
  - CPU & memory availability
  - Node affinity / anti-affinity
  - Taints & tolerations
  - Resource requests

> Scheduler does NOT start containers — it only decides placement.

---

### 4. Controller Manager
Runs multiple controllers that **continuously reconcile desired vs actual state**.

Common controllers:
- Node Controller
- ReplicaSet Controller
- Deployment Controller
- Job Controller

> Controllers are why Kubernetes is *self-healing*.

---

## Worker Node Components (The Muscle)

Worker nodes run application workloads.

---

### 1. kubelet
- Node-level agent
- Communicates with API Server
- Ensures Pods are running as defined
- Reports node and pod status

> kubelet is responsible for Pod lifecycle on a node.

---

### 2. Container Runtime
- Runs containers inside Pods
- Kubernetes uses **CRI (Container Runtime Interface)**

Common runtimes:
- containerd
- CRI-O

> Docker is not required anymore. CRI is the standard.

---

### 3. kube-proxy
- Handles Service networking
- Implements traffic routing using:
  - iptables or
  - IPVS

> kube-proxy enables stable Service IPs and load balancing.

---

## Request Flow (End-to-End)

1. User applies a manifest (`kubectl apply`)
2. API Server validates request
3. Desired state stored in etcd
4. Scheduler selects a node
5. kubelet creates the Pod
6. Container runtime starts containers
7. Controllers continuously monitor state

---

## Key Takeaways

- Kubernetes is **declarative**, not imperative
- Control plane decides — nodes execute
- etcd is the single source of truth
- Controllers keep the system stable
- Architecture knowledge beats YAML memorization

---

## Common Interview Traps

- Confusing kubelet with scheduler
- Thinking Docker is mandatory
- Ignoring etcd importance
- Not understanding reconciliation loops

---

## Final Advice

If you can’t explain Kubernetes architecture **without diagrams or notes**, you don’t truly understand it.

Master the architecture first.  
Everything else builds on top of it.

---

