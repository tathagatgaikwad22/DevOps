# 🔐 RBAC in Kubernetes (Role-Based Access Control)

RBAC in Kubernetes defines **who can do what and where** inside your cluster.  
If RBAC is weak, your cluster security is a joke. Period.

---

## 🚨 Why RBAC Matters

Kubernetes does **not** protect you by default.  
RBAC is the difference between:
- 🔒 Controlled access  
- 💥 Total cluster compromise  

RBAC answers three critical questions:
- 👤 **Who** (User / ServiceAccount)
- 🎯 **What** (verbs like get, list, create, delete)
- 📦 **Where** (namespace or cluster-wide)

---

## ❌ Common RBAC Mistakes

- Giving `cluster-admin` to everyone 👑  
- One role for Dev, Ops, CI/CD, and interns 🤡  
- No namespace isolation 🚪  
- No audits or permission reviews 🫥  

These aren’t shortcuts — they’re security failures.

---

## ✅ Best Practices (Non-Negotiable)

- 🔑 **Least Privilege** – only required permissions  
- 📦 **Namespace-level Roles** instead of ClusterRoles  
- 👥 **Separate roles** for Dev, Ops, CI/CD  
- 🔄 **Regular audits** of roles & bindings  

---

## 🧱 Core RBAC Components

| Component | Purpose |
|---------|--------|
| Role | Permissions inside a namespace |
| ClusterRole | Permissions across the cluster |
| RoleBinding | Assigns Role to user/service |
| ClusterRoleBinding | Assigns ClusterRole |

---

## 🧪 Example: Namespace Role

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: pod-reader
  namespace: dev
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "list"]
```

## Example: RoleBinding
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: read-pods
  namespace: dev
subjects:
- kind: User
  name: dev-user
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```

# ⚠️ Hard Truth
If you don’t understand your RBAC rules,
you don’t control your Kubernetes cluster.
Security by assumption = failure by design.

# 📌 Final Advice
Audit RBAC like you audit money.
Because one wrong permission can burn everything.

# Tags
#kubernetes #rbac #devops #cloudsecurity #platformengineering
