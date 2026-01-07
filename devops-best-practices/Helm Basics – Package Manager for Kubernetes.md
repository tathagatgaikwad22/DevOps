# 🚢 Helm Basics – Package Manager for Kubernetes ☸️

If you’re working with **Kubernetes** and still managing raw YAML files manually,
you’re wasting time and increasing risk.

**Helm** fixes that.

---

## 🔧 What is Helm?
Helm is the **package manager for Kubernetes**, similar to:
- 📦 `apt` for Linux  
- 📦 `npm` for JavaScript  
- 📦 `pip` for Python  

But built specifically for **K8s applications**.

---

## 📦 Helm Charts
A **Helm Chart** is a packaged collection of Kubernetes resources:
- Deployments
- Services
- ConfigMaps
- Secrets

➡️ One chart = one application  
➡️ Reusable, configurable, versioned

---

## 🚀 Why Helm Matters
- ⚡ Faster deployments
- 🔄 Easy upgrades & rollbacks
- 🧹 Less YAML duplication
- 🌍 Environment-based configs (dev / stage / prod)
- 👥 Team-friendly & scalable

---

## 🧠 Mental Model
> Kubernetes is the **engine** 🛠️  
> Helm is the **gearbox** ⚙️  

Running K8s without Helm slows you down.

---

## 📌 Common Helm Commands
```bash
helm install
helm upgrade
helm rollback
helm list

💡 Bottom Line
If you’re serious about Kubernetes,
Helm is not optional.
🚫 Manual YAML sprawl = technical debt
✅ Helm = speed, safety, and sanity
