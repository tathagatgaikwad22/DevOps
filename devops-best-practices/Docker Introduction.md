🐳 Docker Introduction — Complete Guide with Examples

This repository contains a beginner-friendly introduction to Docker, along with commands, Dockerfiles, examples, and best practices. Use this as your learning reference or documentation.


---

📘 What is Docker?

Docker is a containerization platform that packages applications and their dependencies into lightweight, portable containers.
It helps developers and DevOps engineers ensure consistency across environments.


---

🚀 Why Docker?

🚀 Fast & Lightweight

🧩 Portable across systems

🔁 Consistent deployment

🧱 Ideal for microservices

⚙️ Perfect for CI/CD pipelines

☁️ Cloud-native friendly


---


🧱 Docker Components

✔️ Docker Image

A template used to create containers.

✔️ Docker Container

A running instance of an image.

✔️ Dockerfile

A file containing instructions to build images.

✔️ Docker Hub

A cloud registry for images.

✔️ Volumes

Used for data persistence.

✔️ Networks

Used for container communication.


---

📄 Sample Dockerfile

1. Use base image
FROM node:18

2. Set working directory
WORKDIR /app

3. Copy package files
COPY package*.json ./

4. Install dependencies
RUN npm install

5. Copy everything else
COPY . .

6. Expose port
EXPOSE 3000

7. Start the application
CMD ["npm", "start"]


---

🛠️ Build & Run Docker Containers

🔹 Build Image

docker build -t my-node-app .

🔹 Run Container

docker run -d -p 3000:3000 my-node-app

🔹 View Running Containers

docker ps

🔹 Stop Container

docker stop <container-id>

🔹 Remove Container

docker rm <container-id>

🔹 Remove Image

docker rmi my-node-app


---

🔧 Useful Everyday Docker Commands

✔️ List Images

docker images

✔️ Download Image

docker pull nginx

✔️ Run NGINX

docker run -d -p 8080:80 nginx

✔️ Get Container Logs

docker logs <container-id>

✔️ Access Container Shell

docker exec -it <container-id> bash


---

🐳 Docker Compose Example

Create a file named docker-compose.yml:

version: "3.9"

services:
  web:
    image: nginx:latest
    ports:
      - "8080:80"

  app:
    build: .
    ports:
      - "3000:3000"
    volumes:
      - .:/app

Run all services:

docker-compose up -d

Stop all services:

docker-compose down


---

🌟 Docker Best Practices

✔ Use lightweight images (Alpine)
✔ Use .dockerignore to avoid large builds
✔ Keep Dockerfile clean & small
✔ Use multi-stage builds
✔ Never store secrets inside images
✔ Do not run containers as root
✔ Use tagged image versions
✔ Use volumes for data persistence


---

🧠 Tips & Tricks

Clean unused resources

docker system prune -a

Check detailed container info

docker inspect <container-id>

Save an image to a file

docker save -o myapp.tar my-node-app


---

💼 Real-World Use Cases

Microservices architecture

CI/CD pipelines

Local development

Dev/Stage/Prod consistency

Cloud deployments (AWS ECS, EKS, Azure AKS, GCP GKE)

Automated testing environments



---

🎯 Conclusion

Docker simplifies the development and deployment process by providing consistent, portable, and efficient containers.
Mastering Docker opens the door to:

Kubernetes

Microservices

CI/CD automation

Cloud-native DevOps

