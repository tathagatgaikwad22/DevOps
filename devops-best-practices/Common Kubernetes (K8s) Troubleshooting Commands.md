# 🚨 Common Kubernetes (K8s) Troubleshooting Commands

If your Kubernetes cluster breaks and you freeze — you don’t know Kubernetes yet.
These commands are **non-negotiable** for real-world debugging. 🧠🔥

---

## 🔍 Check Cluster State

```bash
kubectl get pods -A
```
👉 View all pods across all namespaces. Always start here.

🧠 Inspect Pod Details
kubectl describe pod <pod-name>
👉 Shows events, errors, and reasons behind pod failures.

📜 View Application Logs
kubectl logs <pod-name>
👉 Debug application-level issues and crashes.

🔄 Logs from Previous Crash
kubectl logs <pod-name> --previous
👉 Useful when pods restart unexpectedly.

🧪 Exec Into a Container
kubectl exec -it <pod-name> -- sh
👉 Inspect the container from inside (no SSH needed).

📦 Service & Endpoint Debugging
kubectl get svc,ep
👉 Verify service-to-pod connectivity.

🧭 Cluster Events (Timeline View)
kubectl get events --sort-by=.metadata.creationTimestamp
👉 Understand what happened and in what order.

⚙️ Resource Usage
kubectl top pod
kubectl top node
👉 Identify CPU & memory bottlenecks.

💡 Reality Check
If you can’t troubleshoot Kubernetes,
you’re not doing K8s — you’re just applying YAML. 📄❌

🏷️ Tags
#kubernetes #devops #cloudnative #sre #k8s
