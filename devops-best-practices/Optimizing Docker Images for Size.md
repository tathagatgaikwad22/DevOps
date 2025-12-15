# Optimizing Docker Images for Size

Bloated Docker images are a **self-inflicted problem**.
If your image is huge, slow, and insecure — that’s not Docker’s fault.  
It’s bad engineering discipline.

This guide explains **how to aggressively reduce Docker image size** using proven, production-ready techniques.

---

## Why Image Size Matters

Large images cause:

- Slow CI/CD pipelines
- Long pull times in production
- Higher storage and network costs
- Bigger attack surface
- Slower scaling and rollbacks

If you care about reliability and speed, you must care about image size.

---

## 1. Choose the Right Base Image

Your base image defines your entire image footprint.

### ❌ Bad
```dockerfile
FROM ubuntu
```
✅ Better

FROM alpine

✅ Best (when possible)

FROM gcr.io/distroless/base-debian12

Rule:
If you don’t need a shell in production, don’t ship one.


---

2. Use Multi-Stage Builds (Mandatory)

Build tools should never be shipped to production.

❌ Bad

FROM golang:1.22
WORKDIR /app
COPY . .
RUN go build -o app
CMD ["./app"]

✅ Good

FROM golang:1.22 AS builder
WORKDIR /app
COPY . .
RUN go build -o app

FROM gcr.io/distroless/base
COPY --from=builder /app/app /app
CMD ["/app"]

Result:

No compiler

No package manager

Only the final binary


This single change can reduce image size by 80–90%.


---

3. Minimize Layers

Each RUN instruction creates a layer. More layers = more size.

❌ Bad

RUN apt update
RUN apt install -y curl

✅ Good

RUN apt update \
    && apt install -y curl \
    && rm -rf /var/lib/apt/lists/*

Always clean package caches. Docker will not do it for you.


---

4. Use .dockerignore (Most People Skip This)

Without .dockerignore, your entire project is sent to Docker.

Example .dockerignore

.git
node_modules
logs
.env
README.md

Smaller build context = faster builds = smaller images.


---

5. Install → Build → Remove

If a tool is only needed for building, remove it after use.

Example (Alpine)

RUN apk add --no-cache build-base \
    && make build \
    && apk del build-base

Temporary dependencies must remain temporary.


---

6. Avoid Unnecessary Packages

If your app needs:

One binary

One runtime


Why are you installing:

curl

vim

bash

net-tools


Containers are not VMs. Stop treating them like one.


---

7. Prefer Static Binaries (When Possible)

Languages like Go allow fully static binaries.

Build example

CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build

Run it in:

FROM scratch
COPY app /app
CMD ["/app"]

You can’t get smaller than this.


---

8. Scan and Measure

Use tools to verify improvements:

docker image ls
docker history <image>

For security:

Trivy

Docker Scout


Smaller images usually mean fewer vulnerabilities.


---

Final Takeaway

Optimizing Docker images is not optional.

If your images are bloated, it means:

You don’t understand Docker layers

You’re careless with production environments

You haven’t optimized your delivery pipeline


Professional engineers build lean, secure, and fast images.

