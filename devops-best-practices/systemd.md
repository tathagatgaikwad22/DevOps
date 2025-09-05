# 🛠️ Managing Services with `systemd`

`systemd` is the default **init system and service manager** in most modern Linux distributions.  
It is responsible for **starting, stopping, monitoring, and managing services** on your system.  

This guide covers **theory, best practices, tips, and tricks** for managing services with `systemd` — useful for DevOps Engineers, SREs, and System Administrators.

---

## 📖 What is `systemd`?

- **Init System** → Initializes the system during boot.  
- **Service Manager** → Controls processes and services (`nginx`, `mysql`, `docker`, etc.).  
- **Framework** → Provides logging (`journald`), timers, dependencies, and resource controls.  

It replaces older init systems like **SysVinit** and is now the standard in **Ubuntu (16+), CentOS/RHEL (7+), Debian (8+), Fedora**, and others.

---

## ⚡ Basic `systemctl` Commands

```bash
# Start / Stop / Restart
systemctl start nginx
systemctl stop nginx
systemctl restart nginx

# Reload configuration without full restart
systemctl reload nginx

# Check status
systemctl status nginx

# Enable/Disable service at boot
systemctl enable nginx
systemctl disable nginx

# View logs for a service
journalctl -u nginx
📂 Anatomy of a systemd Unit File
Unit files define how services behave.
Default locations:

/lib/systemd/system/ → Default system services

/etc/systemd/system/ → Custom/admin services

Example:

[Unit]
Description=My Custom App
After=network.target

[Service]
ExecStart=/usr/local/bin/myapp
Restart=always
User=appuser
Group=appgroup
Environment=APP_ENV=production

[Install]
WantedBy=multi-user.target

🔑 Key Directives:

ExecStart → Command to start service

Restart= → Controls service resilience (always, on-failure)

User/Group → Run with least privilege

Environment → Pass environment variables

After= → Define dependencies

✅ Best Practices
Prefer systemctl over service → Modern, reliable, and widely supported.

Enable only essential services → Reduce attack surface & boot time.

Set restart policies → Use Restart=on-failure or Restart=always.

Apply resource limits in [Service]:

MemoryLimit=512M
CPUQuota=50%
Store custom units in /etc/systemd/system/ → Safe from package updates.

Document services → Use Description= for clarity.

Audit failed services regularly → systemctl --failed.

💡 Pro Tips & Tricks
🔍 Find Failed Services

systemctl --failed

🕒 View Logs from Last Boot

journalctl -b

🔄 Reload Systemd After Changes

systemctl daemon-reload

🛡️ Secure Services

Inside [Service] block:

User=nonrootuser
Group=nonrootgroup
NoNewPrivileges=true

🧹 Mask vs Disable
systemctl disable nginx → Stops auto-start on boot.

systemctl mask nginx → Prevents any start (even manual).

🚀 Why systemd Matters for DevOps/SRE
Ensures resilient, auto-recovering services

Provides centralized logging with journalctl

Enforces security & resource controls

Improves automation & reproducibility across environments

🎯 Summary
Managing services with systemd means more than starting and stopping processes.
It’s about:

Designing reliable and resilient services

Applying least privilege security

Leveraging logs, timers, and dependencies

By mastering systemd, you unlock a powerful toolset to make your infrastructure more robust, secure, and automated.

🧑‍💻 Quick Reference

systemctl start <service>     # Start service
systemctl stop <service>      # Stop service
systemctl restart <service>   # Restart service
systemctl status <service>    # Service status
systemctl enable <service>    # Start at boot
systemctl disable <service>   # Remove from boot
systemctl reload <service>    # Reload config
systemctl --failed            # Check failed services
journalctl -u <service>       # View service logs

🔥 Pro Tip: Combine systemd with monitoring tools like Prometheus + Grafana to track service uptime and failures for production-ready observability.
