# 🐧 ps, top, htop – Linux Monitoring Essentials  

Monitoring processes is a **fundamental skill** for DevOps Engineers, SREs, and SysAdmins.  
Whether debugging high CPU usage, memory leaks, or runaway processes, Linux provides three essential tools:  

- **ps** → Static snapshot of processes  
- **top** → Real-time monitoring  
- **htop** → Interactive and user-friendly monitoring  

This guide explains **theory, best practices, tips, and tricks** for mastering them.  

---

## 🔎 1. ps (Process Status)  

`ps` provides a **one-time snapshot** of running processes.  

### 📌 Common Usage:  
```bash
ps aux             # List all processes with detailed info
ps -eo pid,ppid,stat,cmd   # Custom view with process states
ps -C nginx -o pid,cmd,%mem,%cpu   # Filter by process name

📖 Key Options:
a → All processes

u → User-oriented format (CPU, memory)

x → Processes without a terminal

💡 Tips & Tricks:
Search specific processes:
ps aux | grep python

Sort top CPU consumers:
ps -eo pid,ppid,cmd,%cpu --sort=-%cpu | head

Sort top memory consumers:
ps -eo pid,ppid,cmd,%mem --sort=-%mem | head

🔎 2. top (Real-Time Monitoring)
top provides a dynamic, continuously refreshing view of processes.

📌 Default Columns:
PID → Process ID

USER → Owner

%CPU → CPU usage

%MEM → Memory usage

TIME+ → CPU time used

COMMAND → Executable name

📌 Useful Shortcuts:
M → Sort by memory

P → Sort by CPU

1 → Show per-core CPU usage

k → Kill process by PID

💡 Tips & Tricks:
Run with options for sorted view:

top -o %CPU
top -o %MEM

🔎 3. htop (Interactive Monitoring)
htop is a modern, colorful, and interactive version of top.

📌 Key Features:
F6 → Sort by column

F5 → Tree view (process hierarchy)

F9 → Kill processes easily

F2 → Customize interface (columns, colors, meters)

💡 Tips & Tricks:
Quickly identify Zombie (Z) or Uninterruptible Sleep (D) processes with color-coded output.

Scroll through long process lists more easily than top.

Filter processes interactively by typing their name.

✅ Best Practices for Monitoring
Know the Baseline

Run top/htop during normal loads → helps identify what “healthy” looks like.

Use the Right Tool

ps → Snapshots, scripting, logging.

top → Live system health checks.

htop → Interactive debugging.

Automate Alerts

Don’t rely only on manual checks. Use Prometheus, Grafana, Nagios, or CloudWatch for alerts.

Look for Trends

Short CPU spikes aren’t always bad. Long-term usage growth indicates deeper issues.

Investigate Before Killing

High CPU/memory often = application bug or misconfiguration. Killing is a band-aid, not a fix.

⚡ Pro Commands
Watch a specific process continuously:
watch -n 1 "ps -C nginx -o pid,cmd,%mem,%cpu"

Save process state for later analysis:
ps aux > processes.log

Check top 10 processes by memory and CPU:
ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%mem | head
ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%cpu | head

🧩 Real-World Debugging Example
📌 Scenario: A server slows down.

Run top → CPU at 95%, with a Python script consuming most resources.

Use htop → Discover multiple child processes spawned by the script.

Investigate → Bug in code (while(true) loop).

Fix root cause instead of just killing processes.

👉 Lesson: Monitoring tools detect the symptoms, but engineers must trace the cause.

💡 Key Takeaways
ps = Snapshot monitoring (good for scripting/logging).

top = Real-time monitoring.

htop = Interactive and user-friendly monitoring.

Together, they form the first line of defense for Linux system health and performance.

## 📌 Resources  

- [man ps](https://man7.org/linux/man-pages/man1/ps.1.html)  
- [man top](https://man7.org/linux/man-pages/man1/top.1.html)  
- [htop project](https://htop.dev/)  

👨‍💻 Maintained by Tathagat Gaikwad
📢 Contributions welcome – submit a PR with new tips!

#Linux #DevOps #SRE #SysAdmin #Monitoring #Performance
