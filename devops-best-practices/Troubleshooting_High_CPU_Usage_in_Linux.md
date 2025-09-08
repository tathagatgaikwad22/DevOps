# 🐧 Troubleshooting High CPU Usage in Linux

High CPU usage is a common alert in Linux environments for **DevOps Engineers, SREs, and System Administrators**.  
But here’s the important part: **high CPU usage isn’t always bad**. Sometimes, it’s just your CPU doing its job effectively. Other times, it’s a warning sign of runaway processes, inefficient code, or system misconfiguration.  

This guide will walk you through **theory, step-by-step troubleshooting, best practices, and tips** to deal with high CPU usage like a pro.  

---

## 🔎 Understanding CPU Usage in Linux

Before you troubleshoot, know what CPU metrics mean:  

- **CPU Utilization (%)** → How busy the CPU is.  
- **Load Average** → Number of processes waiting for CPU.  
  - Rule of thumb: If load average > number of CPU cores → bottleneck.  
- **Types of CPU Usage**:  
  - `user` → Applications/processes.  
  - `system` → Kernel tasks.  
  - `iowait` → Waiting on disk/network I/O.  
  - `steal` → Time taken by hypervisor (in VMs).  

👉 **High CPU usage doesn’t always mean a problem**. Distinguish between *healthy usage* vs *bottlenecks*.  

---

## ⚡ Step 1: Identify the Culprit

Start with these commands:

```bash
top
htop
uptime
pidstat -u
ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%cpu | head

top → See real-time processes.

htop → Interactive view with colors.

uptime → Quick load averages.

pidstat → CPU usage per process.

ps → Top CPU-consuming processes.

🧠 Step 2: Deep Dive into CPU Behavior
Go beyond basics:

mpstat -P ALL   # CPU usage per core
iostat -x       # Is it I/O wait instead of CPU?
sar -u 1 5      # CPU utilization over time
perf top        # Which functions/code paths consume CPU
One core maxed out? → Single-thread bottleneck.

High iowait? → Problem is storage, not CPU.

perf top → Debug heavy apps at function level.

🛠️ Step 3: Fix the Problem
1. Runaway Processes
Kill or restart misbehaving processes:

kill -9 <pid>
Then investigate root cause (bad loop, memory leak, query overload).

3. Service Optimization
Tune databases (MySQL/Postgres queries).

Optimize web servers (NGINX, Apache worker configs).

Adjust JVM/Python app resource limits.

3. System Tuning
Lower process priority:

renice -n 10 -p <pid>
Limit process CPU usage:
cpulimit -p <pid> -l 50

4. Scaling
Add more CPU cores.
Use load balancers to distribute traffic.
Offload heavy batch jobs into queues (Kafka, RabbitMQ, Celery).

💡 Best Practices, Tips & Tricks
Baseline first → Know what “normal” CPU usage looks like.

Don’t panic → 90% CPU usage is fine if the system is responsive.

Smart alerts → Alert only when load average > cores and sustained.

Cron jobs → Stagger schedules to avoid CPU spikes.

Containers/K8s → Set CPU requests/limits properly to avoid noisy neighbors.

Logs matter → High CPU may be a symptom (bad code, leaks, runaway queries).

Monitor continuously → Use Prometheus + Grafana for alerts and visualization.

🧭 Key Takeaway
High CPU usage is not always a villain. It could mean:

✅ Your system is simply working efficiently.

⚠️ Or, a misconfigured process, inefficient code, or bottleneck is slowing things down.

The goal isn’t to kill processes blindly, but to diagnose, optimize, and scale.

🔍 Quick Reference Commands

# Check top processes
top -o %CPU
htop

# Load average
uptime

# Per-core usage
mpstat -P ALL

# Per-process usage
pidstat -u

# Limit a process
cpulimit -p <pid> -l 50

🚀 Final Thoughts
The real skill isn’t in running top — it’s in interpreting data, correlating with system behavior, and making smart decisions.

👉 What’s your go-to first command when you see a CPU alert: top, htop, or pidstat?

#Linux #DevOps #SRE #SysAdmin #Troubleshooting #Performance #BestPractices
