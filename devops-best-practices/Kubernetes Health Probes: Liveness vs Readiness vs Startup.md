# Kubernetes Health Probes: Liveness vs Readiness vs Startup 🚦

Kubernetes provides three health probes to manage application lifecycle and traffic safely.
Incorrect probe design is a common cause of pod restarts and downtime.

---

## ❤️ Liveness Probe

**Purpose:** Check if the application is alive or stuck.

**On failure:** Pod is restarted.

**Use for:**
- Deadlocks
- Infinite loops
- Crashed processes

**Do NOT use for:**
- Slow startup
- Temporary dependency failures

```yaml
livenessProbe:
  httpGet:
    path: /health/live
    port: 8080
  initialDelaySeconds: 30
  periodSeconds: 10
```

🚦 Readiness Probe
Purpose: Check if the application can serve traffic.
On failure: Traffic is stopped, pod stays running.
Use for:
Database unavailable
Cache warming
Temporary overload

readinessProbe:
  httpGet:
    path: /health/ready
    port: 8080
  periodSeconds: 5

🚀 Startup Probe
Purpose: Handle slow-starting applications.
On failure: Pod is killed.
Why it matters: Prevents liveness probe from killing the app before startup completes.

startupProbe:
  httpGet:
    path: /health/startup
    port: 8080
  failureThreshold: 30
  periodSeconds: 10

❌ Common Mistakes
Using liveness probe for DB checks
Skipping startup probe for slow apps
Copy-pasting probe configs blindly

✅ Best Practices
Keep probes lightweight
Use separate endpoints
Test probe behavior under failures
