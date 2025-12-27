# Rolling Updates in Kubernetes

Rolling updates allow Kubernetes to update applications **without downtime** by gradually replacing old Pods with new ones. This is the **default and recommended** strategy for production workloads.

---

## How It Works

Kubernetes Deployments manage rolling updates by:
- Creating a new ReplicaSet
- Starting new Pods gradually
- Terminating old Pods gradually
- Maintaining minimum availability

Any change to the Pod template triggers a rolling update.

---

## Basic Example

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-app
spec:
  replicas: 4
  strategy:
    type: RollingUpdate
  template:
    spec:
      containers:
        - name: app
          image: nginx:1.25
```

# RollingUpdate Parameters

maxUnavailable: Max Pods allowed to be unavailable

maxSurge: Extra Pods allowed during update

strategy:
  type: RollingUpdate
  rollingUpdate:
    maxUnavailable: 1
    maxSurge: 1

For 4 replicas:
Minimum Pods: 3
Maximum Pods: 5

# Commands
# Update image:

kubectl set image deployment/web-app app=nginx:1.26

# Monitor rollout:

kubectl rollout status deployment/web-app

# Rollback:

kubectl rollout undo deployment/web-app

# Best Practices
Use readiness probes
Run multiple replicas
Keep maxUnavailable low
Monitor every deployment

# Summary
Rolling updates provide safe, controlled, zero-downtime deployments in Kubernetes. Misconfiguration is the real risk—not the strategy
