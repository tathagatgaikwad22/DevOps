# Docker HEALTHCHECK – Stop Deploying Blind Containers

A container **running** does NOT mean the application is **healthy**.  
Docker will happily keep a broken app alive unless you explicitly tell it how to verify health.

That’s where `HEALTHCHECK` comes in.

---

## What is Docker HEALTHCHECK?

`HEALTHCHECK` defines a command that Docker runs periodically to determine whether a container is:

- `healthy`
- `unhealthy`
- `starting`

Without it, Docker assumes the container is always healthy — which is a dangerous assumption in production.

---

## Why HEALTHCHECK Matters

- Prevents traffic from reaching broken containers
- Enables auto-restart and self-healing
- Improves reliability in Docker Compose, Swarm, and Kubernetes
- Reduces silent failures and late-night incidents

**No healthcheck = blind deployment.**

---

## Basic Syntax

```dockerfile
HEALTHCHECK --interval=30s --timeout=5s --retries=3 \
  CMD curl -f http://localhost:8080/health || exit 1
```
How it works:

Exit code 0 → container is healthy

Exit code 1 → container is unhealthy

Docker tracks failures based on retries



---

Common HEALTHCHECK Options

Option	Description

--interval	Time between checks
--timeout	Max time for a check
--retries	Failures before unhealthy
--start-period	Grace time before checks begin


Example:

HEALTHCHECK --interval=20s --timeout=3s --retries=5 --start-period=10s \
  CMD curl -f http://localhost:8080/health || exit 1


---

Bad Practices (Stop Doing This)

❌ Checking only if the port is open
❌ Using sleep or dummy commands
❌ Ignoring database or external dependencies
❌ Skipping HEALTHCHECK entirely

If your app depends on a DB, cache, or message queue — validate them.


---

Good HEALTHCHECK Design

✔ Use a real /health or /ready endpoint
✔ Keep checks lightweight and fast
✔ Fail fast when critical dependencies are down
✔ Avoid heavy queries or long-running logic


---

Example: Application + Database Check

HEALTHCHECK CMD \
  curl -f http://localhost:8080/health && \
  pg_isready -h localhost -p 5432 || exit 1

This ensures:

App is responding

Database is reachable



---

Disabling HEALTHCHECK (Rarely Needed)

HEALTHCHECK NONE

Use this only when:

Health is managed externally

The container truly doesn’t need monitoring


Otherwise, don’t be lazy.


---

Docker Compose Example

services:
  app:
    image: myapp
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:8080/health"]
      interval: 30s
      timeout: 5s
      retries: 3

Compose can now wait for healthy containers before starting dependencies.


---

HEALTHCHECK vs Kubernetes Probes

Docker	Kubernetes

HEALTHCHECK	livenessProbe / readinessProbe
Single check	Separate liveness & readiness
Container-level	Pod-level control


In Kubernetes, always split liveness and readiness.


---

Final Takeaway

If you ship containers without HEALTHCHECK:

You’re guessing

You’re increasing downtime

You’re asking for production failures


HEALTHCHECK is not optional. It’s basic engineering discipline.

