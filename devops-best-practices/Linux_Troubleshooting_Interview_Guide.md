# 🐧 Linux Troubleshooting Interview Guide

A complete resource for **DevOps, SRE, Cloud, and SysAdmin interviews**.  
This guide covers **15 common Linux troubleshooting questions** with **theory, best practices, tips, and tricks**.  

---

## 🔎 1. The server feels slow. How do you start troubleshooting?  
**Theory:** Slowness often comes from CPU spikes, memory leaks, disk I/O bottlenecks, or runaway processes.  

**Best Practices:**
- Start broad (system-level monitoring) → narrow down to specific processes.
- Don’t kill processes without knowing their role.  

**Tips & Tricks:**
```bash
top / htop       # Real-time CPU & memory
vmstat 5         # System performance
iostat -xz 5     # Disk I/O
kill -15 <pid>   # Graceful termination
kill -9 <pid>    # Force kill (last resort)

🌐 2. The server cannot reach the internet.
Theory: Network troubleshooting works in layers → Interface → Route → DNS → Firewall.

Best Practices:
Validate connectivity before debugging DNS.
Go from low-level checks to high-level services.

Tips & Tricks:
ip a                # Network interfaces
ping 8.8.8.8        # Test raw connectivity
ping google.com     # Test DNS resolution
ss -tulnp           # Check listening ports
iptables -L         # Firewall rules

📂 3. Disk space is full.
Theory: Logs, cache, or large files usually consume space.

Best Practices:
Investigate the cause (log rotation, cleanup).
Don’t delete random files blindly.

Tips & Tricks:
df -h                         # Disk usage
du -sh * | sort -h            # Largest directories
lsof | grep deleted           # Deleted-but-held files
journalctl --vacuum-time=7d   # Clear old logs

🔑 4. “Permission denied” even as root.
Theory: Permissions are enforced by:
File permissions (rwx)
Ownership (user:group)
SELinux/AppArmor contexts

Best Practices:
Check SELinux/AppArmor context, not just file mode.

Tips & Tricks:
ls -l                 # Permissions
ls -Z                 # SELinux context
chmod 755 file        # Adjust permissions
chown user:group file # Fix ownership

⚡ 5. A service won’t start.
Theory: Causes → bad configs, missing dependencies, port conflicts.

Best Practices:
Always check logs before restarting.
Verify service dependencies.

Tips & Tricks:
systemctl status nginx     # Check service
journalctl -xe             # Logs
ss -tulnp                  # Port conflicts

🖥️ 6. The server doesn’t boot.
Theory: Boot failures → GRUB errors, kernel panic, fstab misconfig.

Best Practices:
Boot into rescue/recovery mode.
Fix fstab or kernel modules step by step.

Tips & Tricks:
journalctl -xb    # Boot logs
dmesg | less      # Kernel messages
📡 7. DNS resolution fails but IP works.
Theory: DNS service misconfiguration or broken /etc/resolv.conf.

Best Practices:
Check if DNS servers are reachable.

Tips & Tricks:
cat /etc/resolv.conf
dig google.com
nslookup google.com

🧵 8. High CPU usage by a single process.
Theory: Often caused by runaway loops or misconfigurations.

Best Practices:
Analyze the process before killing.

Tips & Tricks:
top
pidstat -p <pid>
strace -p <pid>   # Trace syscalls

🗂️ 9. Filesystem mounted as read-only.
Theory: Kernel remounts read-only if corruption detected.

Best Practices:
Run fsck in rescue mode.

Tips & Tricks:
dmesg | grep error
fsck /dev/sda1
🛠️ 10. SSH login is slow.
Theory: Caused by DNS reverse lookup or GSSAPI authentication.

Best Practices:
Disable unused options in /etc/ssh/sshd_config.

Tips & Tricks:
ssh -vvv user@host
# In sshd_config
UseDNS no
GSSAPIAuthentication no

🧮 11. Memory usage is high.
Theory: Could be real leaks or just caching.

Best Practices:
Differentiate cache vs application memory.

Tips & Tricks:
free -m
ps aux --sort=-%mem
smem

🗄️ 12. Logs are not updating.
Theory: Common causes → log rotation, wrong permissions, or service writing elsewhere.

Best Practices:
Check if process still has file handle open.

Tips & Tricks:
ls -l /var/log
lsof | grep log

⚙️ 13. Cron job is not running.
Theory: PATH issues, permissions, or cron service down.

Best Practices:
Always use absolute paths in cron scripts.

Tips & Tricks:
systemctl status cron
tail -f /var/log/cron
crontab -l

🔍 14. Kernel panic occurred.
Theory: Faulty drivers, corrupted kernel, or hardware issues.

Best Practices:
Collect panic logs for root cause analysis.

Tips & Tricks:
dmesg
cat /var/log/messages

🧑‍💻 15. How to approach troubleshooting in interviews?
Theory: It’s not about memorized commands—it’s about structured thinking.

Framework:

Logs → Processes → Services → Configs → Dependencies

Best Practices:

Think out loud, explain elimination steps.

Show automation mindset (scripts, Ansible, monitoring).

🧠 Interview Pro-Tips
✅ Think Out Loud → Walk through reasoning.

✅ Don’t Panic → Describe logical approach if stuck.

✅ Prioritize Impact → Minimize downtime.

✅ Automate Where Possible → Scripts, playbooks, monitoring.

🔖 Final Takeaway
Linux troubleshooting is about systematic problem-solving, not memorization.
If you approach issues with layered debugging + best practices, you’ll stand out in interviews and in real-world firefighting.

💬 Contribute
Have a tricky Linux troubleshooting question that should be added here?
Open a PR or raise an issue!

#Linux #DevOps #SRE #SysAdmin #Cloud #Troubleshooting #Interview
