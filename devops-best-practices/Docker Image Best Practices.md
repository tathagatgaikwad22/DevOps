🐳 Docker Image Best Practices

Building efficient, secure, and maintainable Docker images is non-negotiable for any serious DevOps or software engineering workflow.
This guide outlines the most important best practices you should follow.


---

⚡ 1. Use the Smallest Base Image Possible

Avoid heavy base images like ubuntu:latest unless absolutely needed.

Prefer minimal images such as:

alpine

debian:slim

Language-specific slim variants (python:3.12-slim, node:20-alpine, etc.)


Benefits: Faster builds, quicker pulls, fewer vulnerabilities.



---

🧱 2. Use Multi-Stage Builds

Multi-stage builds help you separate build dependencies from runtime dependencies.

Example:

FROM golang:1.22 AS builder
WORKDIR /app
COPY . .
RUN go build -o app

FROM alpine
COPY --from=builder /app/app /usr/local/bin/app
CMD ["app"]


---

🔐 3. Pin Versions — Avoid “latest”

Never use latest for OS, tools, or runtime images.

Always pin tags and package versions to avoid unexpected build failures.



---

🗂️ 4. Minimize Layers & Clean Up Within the Same Layer

Every command creates a new layer unless chained.

RUN apt-get update \
    && apt-get install -y curl \
    && rm -rf /var/lib/apt/lists/*


---

👤 5. Drop Root Privileges

Running your container as root is a security risk.

RUN adduser -D appuser
USER appuser


---

📦 6. Copy Only What You Need

Avoid blindly using:

COPY . .

Use a properly configured .dockerignore file to avoid sending:

node_modules

logs

local environment files

build artifacts



---

⚙️ 7. Add HEALTHCHECK Instructions

Health checks help detect silent failures.

HEALTHCHECK --interval=30s --timeout=3s \
  CMD curl -f http://localhost:8080/health || exit 1


---

🧹 8. Scan Images for Vulnerabilities

Use tools such as:

Trivy

Grype

Docker Scout


Integrate scanning into CI/CD.


---

📉 9. Keep Images Lean

Remove unused dependencies.

Split responsibilities across multiple services where possible.

Inspect your image size regularly using:


docker image ls
docker history <image>


---

🧩 Final Notes

A Docker image is not just a packaging artifact — it’s part of your application’s reliability and security posture.
Follow these practices consistently to ship faster, safer, and more maintainable software.

