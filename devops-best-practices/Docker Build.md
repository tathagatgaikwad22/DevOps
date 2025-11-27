🚀 Docker Build Best Practices

Containerizing your application isn’t the goal — shipping fast, secure, reproducible images is.
Most teams unknowingly build slow, bloated, and vulnerable images. This guide fixes that.


---

🔹 1. Use Minimal & Explicit Base Images

Avoid heavy images like:

FROM node:latest
FROM python:latest

Use lighter, predictable images:

FROM node:20-alpine
FROM python:3.12-slim

Why:

Smaller attack surface

Faster builds & pulls

More deterministic behavior



---

🔹 2. Use Multi-Stage Builds (Non-Negotiable)

Cut out unnecessary build tools from final images.

Example:

# Build stage
FROM node:20-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

# Final stage
FROM node:20-alpine
WORKDIR /app
COPY --from=builder /app/dist ./dist
CMD ["node", "dist/index.js"]

Benefits:

Massive reduction in image size

Cleaner, production-only final image



---

🔹 3. Avoid COPY . . — Use .dockerignore

Mindlessly copying everything increases build time and context size.

Create a .dockerignore:

node_modules
.git
.env
dist
logs
*.md

Copy only what is required.


---

🔹 4. Optimize Layer Caching

A rookie mistake is placing dependency installation AFTER code copy:

❌ Bad:

COPY . .
RUN npm install

This breaks cache every commit.

✅ Good:

COPY package*.json ./
RUN npm ci
COPY . .

Result:

10× faster Docker builds

CI/CD pipelines stop feeling sluggish



---

🔹 5. Pin Versions for Reproducibility

Never trust “latest”.

Pin tools & OS packages:

RUN apk add --no-cache curl=8.5.0-r0

Pin dependencies (package-lock.json, pip freeze, etc.).

Why:

Avoid random failures

Ensure predictable builds across environments



---

🔹 6. Scan Images for Vulnerabilities

Use tools like:

Trivy

Grype

Snyk

GitHub’s built-in scanners


Example:

trivy image myapp:latest

If you’re not scanning, you’re shipping vulnerabilities — period.


---

🔹 7. Do Not Run Containers as Root

Running as root is convenient… and a security hazard.

RUN adduser -D appuser
USER appuser

Impact:

Reduced damage if compromised

Better security posture



---

🔹 8. Add Useful Labels (Metadata Matters)

LABEL org.opencontainers.image.title="myapp" \
      org.opencontainers.image.source="https://github.com/your/repo" \
      org.opencontainers.image.version="1.0.0"

Pays off when debugging, scanning, or automating.


---

🔹 9. Keep Images Small & Clean

Tips:

Prefer Alpine / Slim images

Remove build caches

Clean temporary files

Avoid installing unnecessary packages



---

🔹 10. Use Healthchecks (Optional but Strongly Recommended)

HEALTHCHECK --interval=30s --timeout=3s \
  CMD curl -f http://localhost:3000/health || exit 1

Helps orchestrators restart unhealthy containers quickly.


---

✅ Summary

High-quality Docker images aren’t built by accident.
They are the result of:

Minimal, well-chosen base images

Multi-stage builds

Proper caching

Security scanning

Non-root execution

Clean layering and metadata


Good images make deployments faster, safer, and easier to maintain.
