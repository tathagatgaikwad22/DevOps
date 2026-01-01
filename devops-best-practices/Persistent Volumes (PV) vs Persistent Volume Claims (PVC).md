# Persistent Volumes (PV) vs Persistent Volume Claims (PVC)

Kubernetes Pods are **ephemeral**.  
Your data **must not be**.

To solve this, Kubernetes separates **storage from compute** using **Persistent Volumes (PV)** and **Persistent Volume Claims (PVC)**.

---

## Why PV & PVC Exist

Pods can be restarted, rescheduled, or deleted at any time.  
If storage were tied directly to Pods, **data loss would be inevitable**.

Kubernetes fixes this by introducing an abstraction layer for storage.

---

## Persistent Volume (PV)

A **Persistent Volume (PV)** represents **actual physical storage** available to the cluster.

### Key Characteristics
- Cluster-level resource
- Provisioned by administrators or dynamically
- Backed by real storage:
  - AWS EBS
  - GCP Persistent Disk
  - Azure Disk
  - NFS, iSCSI, etc.
- Exists independently of Pods

### Common Properties
- Capacity (e.g. `10Gi`)
- Access Modes (`ReadWriteOnce`, `ReadOnlyMany`, `ReadWriteMany`)
- Reclaim Policy (`Retain`, `Delete`, `Recycle`)

> **Reality:** A PV does nothing until it is claimed.

---

## Persistent Volume Claim (PVC)

A **Persistent Volume Claim (PVC)** is a **request for storage**, not storage itself.

### What a PVC Specifies
- Required storage size
- Required access mode
- Storage class (optional)

### Key Characteristics
- Namespace-scoped
- Created by developers
- Abstracts infrastructure details

> **Reality:** PVCs don’t store data — they request it.

---

## PV–PVC Binding Process

1. PVC is created
2. Kubernetes looks for an available PV
3. Matching is done based on:
   - Size
   - Access mode
   - Storage class
4. A **one-to-one binding** is created

Once bound, the PV is **locked** to that PVC.

---

## StorageClass & Dynamic Provisioning

In modern Kubernetes clusters, PVs are usually created automatically.
PVC → StorageClass → PV (auto-created)

### Benefits
- No manual PV creation
- Scales automatically
- Cloud-native approach

> Most production clusters rely on dynamic provisioning.

---

## How Pods Use Storage
Pods **never reference PVs directly**.

They reference a PVC:
Pod → PVC → PV → Physical Storage

This design keeps applications portable and infrastructure-agnostic.

---

## Common Mistakes

- ❌ Mounting a PV directly in a Pod
- ❌ Assuming PVC stores data
- ❌ Ignoring access modes
- ❌ Deleting a PVC and expecting data to remain (`Delete` reclaim policy)

---

## Quick Comparison

| Component | Role |
|--------|------|
| PV | Actual storage |
| PVC | Request for storage |
| Pod | Uses the claim |

---

## One-Line Takeaway

> **PV is the storage.  
> PVC is the request.  
> Pod is the consumer.**

Understand this, and Kubernetes storage stops being confusing.
