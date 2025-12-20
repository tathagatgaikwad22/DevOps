# Writing Your First `deployment.yaml` (Kubernetes)

Writing your first Kubernetes Deployment is **not about YAML syntax**.  
It’s about understanding the *contract* you create with the cluster.

This document explains what each part of a `deployment.yaml` actually does, why it exists, and where beginners usually fail.

---

## What Is a Deployment?

A **Deployment** manages application lifecycle by controlling:
- ReplicaSets
- Pod creation
- Scaling
- Rolling updates
- Self-healing

**Hierarchy**

Deployment └── ReplicaSet └── Pods

You never manage Pods directly in real systems.  
Deployments do that for you.

---

## Minimal Deployment Example

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
  labels:
    app: my-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-app-container
        image: nginx:1.25
        ports:
        - containerPort: 80
```
This is the minimum you should understand — not blindly copy.


---

Breakdown of Each Section

1. apiVersion

Defines which Kubernetes API version you are using.

apiVersion: apps/v1

Controls behavior and features

Wrong version = deprecated or broken resources



---

2. kind

Defines the resource type.

kind: Deployment

You are not creating Pods.
You are creating a controller that manages Pods.


---

3. metadata

Identity and grouping.

metadata:
  name: my-app
  labels:
    app: my-app

Names must be unique per namespace

Labels are critical for selectors and services


Bad labels = operational chaos.


---

4. spec.replicas

Desired number of Pods.

replicas: 3

Kubernetes will always try to maintain this count

Pods crash? Kubernetes replaces them automatically


This is your availability guarantee.


---

5. selector

Links the Deployment to its Pods.

selector:
  matchLabels:
    app: my-app

⚠️ Selector must match Pod labels exactly
Mismatch = Deployment that never controls its Pods.


---

6. template

Blueprint for Pod creation.

template:
  metadata:
    labels:
      app: my-app

Everything under template defines:

How Pods are created

What containers run

How they behave



---

7. containers

Defines what actually runs.

containers:
- name: my-app-container
  image: nginx:1.25

Rules you should follow immediately

Never use latest in production

Always pin image versions

One responsibility per container



---

Adding Resource Management (Important)

If you skip this, you’re not production-ready.

resources:
  requests:
    cpu: "100m"
    memory: "128Mi"
  limits:
    cpu: "500m"
    memory: "256Mi"

Why this matters:

Scheduler placement accuracy

Prevents noisy neighbor problems

Controls cloud costs



---

Common Beginner Mistakes

Using latest image tag

No resource requests or limits

Random or inconsistent labels

Not understanding selector logic

Thinking Deployment = Pod


These mistakes show instantly in interviews.


---

What Happens When a Pod Crashes?

1. kubelet reports failure


2. Deployment notices replica mismatch


3. New Pod is created automatically


4. Desired state is restored



This is self-healing, not magic.


---

Final Advice

If you can’t explain:

Why a ReplicaSet exists

How selectors work

What happens during a Pod failure


Then you’re not “writing” Deployments — you’re copying them.

Master the behavior first.
YAML is just the interface.


---

