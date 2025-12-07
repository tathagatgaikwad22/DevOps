# Docker Resource Limits (CPU & Memory)

Managing resource limits is essential for running stable and predictable Docker containers.  
Without proper limits, a single container can consume excessive CPU or memory, impacting overall system performance.

---

## 📌 Why Resource Limits Matter
- Prevent a container from hogging all CPU cores  
- Avoid system-wide crashes caused by memory leaks  
- Ensure consistent performance across services  
- Protect the host from OOM (Out-Of-Memory) events  

---

## 🖥️ CPU Limits

By default, a Docker container can use **all available CPU cores**.  
Setting CPU limits ensures fair usage and predictable performance.

### **Limit CPU Usage**

```bash
# Limit container to 0.5 CPU (50% of a core)
docker run --cpus="0.5" nginx
```
Assign Specific CPU Cores

# Pin container to CPU core 0 and 1
docker run --cpuset-cpus="0,1" nginx

Why CPU Limits Matter

Prevent noisy-neighbor issues

Improve resource planning

Useful for multi-tenant or production servers



---

🧠 Memory Limits

Memory works differently from CPU —
if a container exceeds its memory limit, it is terminated (OOMKilled).

Set a Hard Memory Limit

docker run -m 512m nginx

Set Soft + Hard Memory Limits

docker run -m 1g --memory-reservation=512m nginx

🔹 Soft limit (memory-reservation): Preferred minimum amount
🔹 Hard limit (-m): Maximum usage; crossing this kills the container

Why Memory Limits Matter

Protects host machine RAM

Prevents memory leaks from taking down the system

Ensures stable container scheduling



---

📊 Monitoring Resource Usage

Check live resource usage:

docker stats

Shows CPU %, memory usage, I/O and more.


---

✅ Best Practices

Always set memory limits for production containers

Use CPU limits when performance predictability is required

Combine soft + hard memory limits

Use monitoring tools (Prometheus, Grafana, cAdvisor)

Test limits under load before deploying to production



---

📚 References

Docker Docs: https://docs.docker.com/config/containers/resource_constraints/



---

📦 Conclusion

Resource limits are not optional for serious deployments.
They ensure containers behave predictably, protect the host, and prevent unexpected system outages.
