# 🖥️ SysAdmin Daily Checklist: The Complete Cheat Sheet  

Being a System Administrator is like being the unseen guardian of an IT ecosystem. Your role ensures servers are up, applications are responsive, data is secure, and users can get their work done without interruptions.  

But here’s the reality: **a single overlooked detail can cause major outages or security breaches.**  

That’s why having a **Daily SysAdmin Checklist** is not just useful — it’s essential. This guide walks you through the *theory, best practices, and pro tips* for building and following a daily routine that keeps systems stable and secure.  

---

## 📖 Why SysAdmins Need a Daily Checklist  

- **Consistency** → Reduces human error by ensuring no step is missed.  
- **Proactive Monitoring** → Catches potential issues before they escalate.  
- **Accountability** → Creates logs and documented routines for audits.  
- **Efficiency** → Saves time by standardizing checks instead of ad-hoc troubleshooting.  

Think of it like a **pilot’s pre-flight checklist** — small details that prevent disasters.  

---

## ✅ The SysAdmin Daily Checklist  

### 🔹 1. System Health Monitoring  
- Check CPU and memory usage (`top`, `htop`, `free -m`)  
- Monitor disk usage (`df -h`) to avoid sudden “out of space” errors  
- Verify system load averages with `uptime`  

💡 *Pro Tip*: Automate alerts with monitoring tools like **Prometheus + Grafana** for real-time dashboards.  

---

### 🔹 2. Logs Review  
- Review `/var/log/syslog`, `/var/log/messages`, `/var/log/auth.log` for anomalies  
- Watch for repeated **failed login attempts** → possible brute-force attacks  
- Check for service crashes or unexpected restarts  

💡 *Trick*: Use `logwatch` or centralize logs with **ELK (Elasticsearch, Logstash, Kibana)**.  

---

### 🔹 3. Security Checks  
- Validate firewall rules are still active (`iptables -L` or `ufw status`)  
- Inspect intrusion detection system (IDS) or SIEM alerts  
- Track user logins with `last` and `who`  

💡 *Best Practice*: Enforce **MFA (multi-factor authentication)** for remote SSH access.  

---

### 🔹 4. Services & Processes  
- Ensure critical services (web server, database, application server) are running  
- Use `systemctl status <service>` to verify uptime  
- Restart failed services promptly  

💡 *Pro Tip*: Configure **systemd service restart policies** (`Restart=always`) to self-heal failed processes.  

---

### 🔹 5. Backups Verification  
- Confirm scheduled backups completed successfully  
- Test restoring a small file or database weekly to validate integrity  

💡 *Best Practice*: Follow the **3-2-1 backup rule** → 3 copies, 2 different media, 1 offsite.  

---

### 🔹 6. Updates & Patch Management  
- Check pending security updates (`apt list --upgradable` / `yum check-update`)  
- Apply patches in staging before production  
- Schedule patch windows for critical fixes  

💡 *Trick*: Automate patch alerts using **Ansible or Puppet**.  

---

### 🔹 7. Networking Health  
- Test connectivity (`ping`, `traceroute`)  
- Monitor bandwidth usage to detect abnormal spikes  
- Check DNS resolution with `dig` or `nslookup`  

💡 *Pro Tip*: Use **Nagios, Zabbix, or Netdata** for proactive network monitoring.  

---

### 🔹 8. Automation & Scheduled Jobs  
- Review `cron` jobs for success/failure  
- Check logs of automation tools like Ansible, Jenkins, or custom scripts  
- Verify monitoring alerts are being sent  

💡 *Best Practice*: Document all scheduled jobs in a **runbook** for quick recovery if something breaks.  

---

## ⚡ Quick Command Cheat Sheet  

```bash
# System health
top
df -h
uptime

# Review logs
tail -f /var/log/syslog

# Security check
grep "Failed password" /var/log/auth.log

# Service status
systemctl status nginx

# Verify backups
ls -lh /backup/
```

---

## 🔒 Pro Tips & Tricks for Better SysAdmin Habits  

- Automate wherever possible — **manual checks don’t scale**.  
- Maintain a **ticketing system (like Jira/ServiceNow)** for tracking daily checks.  
- Create **alerts + dashboards** so you act before users complain.  
- Document your runbook — “tribal knowledge” should not live only in your head.  

---

## 🚀 Final Takeaway  

A SysAdmin’s day is full of firefighting, but a **daily checklist turns firefighting into fire prevention.**  

By proactively monitoring health, reviewing logs, enforcing security, and validating backups, you build resilient systems and reduce downtime.  

---

## 📌 Contribute  

This checklist is open for contributions! Feel free to fork, improve, or suggest additions via pull requests.  

#SysAdmin #DevOps #Linux #BestPractices #ITOps #Automation  
