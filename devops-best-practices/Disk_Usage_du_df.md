# 📊 Disk Usage Analysis in Linux with `du` and `df`

Efficient disk space management is crucial for **SysAdmins, DevOps Engineers, Cloud Engineers, and SREs**.  
Running out of disk space can cause failed deployments, service crashes, and even outages.  

Linux provides two fundamental tools to help analyze and troubleshoot disk space issues:  
- **`du` (Disk Usage)** → *what is consuming disk space*  
- **`df` (Disk Free)** → *how much space is left on mounted filesystems*  

This guide explains their usage with **theory, best practices, tips, and tricks**.

---

## 🔹 Understanding the Tools

### `du` — Disk Usage
- Reports **space used by files and directories**.
- Works recursively, drilling into subdirectories.
- Great for finding **space hogs**.

Example:
```bash
du -sh /var/log
Output:

200M    /var/log
df — Disk Free

Reports free and used space on filesystems.
Useful for getting a system-wide storage overview.
Doesn’t show what is using the space.

Example:
df -h
Output:

Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        40G   28G   10G  74% /
tmpfs           2.0G   60M  1.9G   3% /run

🔑 When to Use What
Use du → to find where space is going.
Use df → to see how much space is left overall.

✅ Combine both for a complete picture.
✅ Best Practices for Disk Usage Analysis

Use Human-Readable Flags
du -sh /home/user
df -h

Find Top Space Consumers
du -ah /var | sort -rh | head -n 20
→ Shows top 20 largest files/directories.

Exclude Other Filesystems
du -x /
→ Keeps analysis within the root filesystem.

Automate Disk Checks
Use a cronjob or systemd timer:
df -h | mail -s "Disk Report" admin@example.com

Integrate with Monitoring Tools
Prometheus
Grafana
Nagios
→ Helps visualize and alert before space runs out.

⚡ Tips & Tricks
Interactive View with ncdu

sudo apt install ncdu
ncdu /
Search Large Files of a Type

du -ah / | grep '\.log$' | sort -rh | head -n 10
Cloud-Specific Advice

AWS/GCP/Azure → Watch EBS/volume limits.
Kubernetes → Check PVCs and pod quotas.

🚀 Pro Guide to Avoid Disk Full Incidents
Be proactive → monitor disk usage regularly.
Automate log rotation & cleanup (logrotate, cron jobs).
Scale cloud volumes early before hitting limits.
Educate teams → developers should know how build artifacts, logs, and caches impact disk usage.

🔑 Key Takeaway
df → tells you how much space you have left.
du → tells you what’s taking up the space.
Together, they’re your first line of defense against downtime caused by full disks.

💬 Discussion
What’s your go-to method for finding disk space hogs?
Do you prefer CLI-only (du, df, ncdu) or pair them with dashboards (Grafana, Prometheus)?

🏷️ Tags
Linux DevOps Cloud SRE Disk Usage du df System Admin
