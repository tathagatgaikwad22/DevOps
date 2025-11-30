# Docker Networking Basics

Docker networking decides **how containers talk to each other, the host, and the outside world**. If you’re building anything beyond a single container, you need to understand this properly.

---

## 🔧 Why Docker Networking Matters
- Controls communication paths  
- Enables isolation and security  
- Allows multi-container applications  
- Provides flexibility in deployments  

---

## 🏗️ Docker Network Types

### 1. Bridge Network (Default)
A virtual network created by Docker.  
Containers on the same bridge can communicate directly.

**Use cases:**
- Local development  
- Multi-container setups  

**Key feature:**  
Supports port mapping using `-p`.

**Example:**
```bash
docker run -d --name web -p 8080:80 nginx
```

---

2. Host Network

The container shares the host’s network namespace.

Pros:

No network translation

Lowest latency


Cons:

Reduced isolation

Port conflicts if multiple services use same port


Example:

docker run --network host nginx


---

3. None Network

The container has no network access.

Use cases:

Security-hardened tasks

Batch jobs not needing network


Example:

docker run --network none alpine


---

4. User-Defined Bridge Networks

Custom networks you create.

Benefits:

Built-in DNS for service discovery

Cleaner architecture

Stronger isolation


Example:

docker network create mynet
docker run -d --name app1 --network=mynet nginx
docker run -d --name app2 --network=mynet alpine sleep 999

Ping between containers:

docker exec -it app2 ping app1


---

5. Overlay Networks

Used for multi-host communication (Docker Swarm).

When you need it:

Scaling services across multiple machines

Distributed microservices


Example (Swarm):

docker network create -d overlay myoverlay


---

🔍 Docker DNS (Service Discovery)

Docker automatically assigns DNS names to containers on the same user-defined network.

Example:

app1 can reach app2 just by using:

curl http://app2


No IP memorization required.


---

🧠 Key Principles to Remember

Docker networks isolate communication.

User-defined networks give you DNS + better structure.

Host mode removes Docker’s network isolation layer.

Overlay networks are for multi-node clusters.

“None” means no networking at all.



---

🧪 Quick Hands-On Test

Try this to verify your understanding:

docker network create testnet
docker run -d --name service1 --network=testnet nginx
docker run -it --name debug --network=testnet alpine sh

Then inside the Alpine container:

ping service1

If this works, you understand the basics.
If not — revisit the concepts.


---

📌 Summary

Docker networking is not magic. It’s a structured system that, once understood, gives you predictable and stable deployments. Start with bridge networks, move to custom ones, then explore overlay when scaling.
