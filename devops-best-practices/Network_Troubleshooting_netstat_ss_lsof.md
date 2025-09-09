# 🌐 Network Troubleshooting with `netstat`, `ss`, and `lsof`  

When production breaks, network issues are among the trickiest to debug. A service might fail to start because a port is already in use, latency might spike due to too many open connections, or you may notice suspicious connections hogging resources.  

As a **DevOps, Cloud, or SRE engineer**, you need fast and reliable ways to analyze and resolve these issues. On Linux, three powerful tools help you get the job done:  

- 🔹 `netstat` – the classic tool (legacy, but still useful)  
- 🔹 `ss` – the modern and faster replacement  
- 🔹 `lsof` – the detective for process ↔ port mapping  

This guide dives deeper into their usage, **theory**, **best practices**, and **real-world tips**.  

---

## 📚 Why These Tools Matter  

Linux networking issues usually map to **TCP/UDP ports and processes**. Common troubleshooting questions include:  

- Is the service **listening on the correct port**?  
- Are there too many connections in states like `TIME_WAIT` or `CLOSE_WAIT`?  
- Which **process** owns the port?  
- Is the system **overloaded with connections**?  

---

## 🛠️ Tool 1: `netstat` – Old but Gold  

`netstat` (network statistics) is one of the oldest tools for network debugging.  

**Example:**  
```bash
netstat -tulnp
Flags:

-t → TCP

-u → UDP

-l → Listening

-n → Numeric output (faster, no DNS resolution)

-p → Show process info

👉 Use case: Identify open ports and the process bound to them.

⚠️ Note: netstat is deprecated in many modern distros.

🛠️ Tool 2: ss – The Modern Replacement
ss (socket statistics) is faster, lighter, and more powerful than netstat. It can handle thousands of sockets easily.

Examples:
Show all listening ports: ss -tulwn
Show active established TCP connections: ss -tan state established
Find the process using port 8080: ss -ltnp sport = :8080
👉 Use case: High-performance troubleshooting in production.

🛠️ Tool 3: lsof – The Detective
In Linux, everything is a file, including sockets. lsof (list open files) links ports back to processes.

Examples:
Find what’s using port 80: lsof -i :80
Show all network connections by a specific user: lsof -u <username> -i
👉 Use case: Debugging “Address already in use” errors, tracing process-level ownership of ports.

📊 Quick Comparison
Feature	netstat	ss	lsof
Speed	Slower on large systems	Very fast & efficient	Moderate
Status	Deprecated in many distros	Actively maintained	Active
Focus	Connections & ports	Sockets, states, performance	Process ↔ Port mapping
Best Use	Legacy / quick checks	General troubleshooting	Debugging port conflicts

💡 Best Practices & Pro Tips
✔ Start with ss → It’s fast and modern.
✔ Use lsof when tracing a port back to a process.
✔ Combine with grep for filtering: ss -tulwn | grep 8080
✔ Check TCP states like TIME_WAIT or CLOSE_WAIT for hints about application behavior.
✔ Cross-check with firewalls (iptables / nftables) → Sometimes ports are open but blocked.
✔ Automate repetitive checks via shell scripts or monitoring.
✔ Audit open ports regularly to catch suspicious processes.

🚨 Real-World Scenarios
“Port already in use” error

lsof -i :8080 → find the process → kill or reconfigure.

Slow web service

ss -s → summary of TCP connections.

Look for high numbers of TIME_WAIT states.

Suspicious remote connections

ss -tunap → see foreign IPs & processes.

Validate against firewall rules and IDS tools.

🧭 Key Takeaways
netstat → Legacy, simple checks.

ss → Fast, modern, detailed.

lsof → Perfect for process ↔ port troubleshooting.

Together, they form a powerful toolkit for network troubleshooting in Linux.

🔖 Further Reading
man ss – socket statistics documentation

man lsof – list open files

Linux Performance Tuning Guides

✍️ Author
Shared by Tathagat Gaikwad — documenting DevOps/SRE/Linux learnings.

#Linux #DevOps #Cloud #SRE #SysAdmin #Networking #Troubleshootin
