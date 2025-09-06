# 🔐 SSH Security Best Practices  
*A DevOps / SRE / Cloud Engineer’s Guide*  

---

## 📖 Overview  

SSH (Secure Shell) is the backbone of secure remote administration.  
It allows us to log into servers, transfer files, and execute commands over an untrusted network.  

But here’s the challenge → **a misconfigured SSH setup is one of the most common entry points for attackers.**  
This guide covers **theory + practical best practices + pro tips** to help you secure SSH access in real-world environments.  

---

## 🚨 Why SSH Security Matters  

Attackers scan the internet **24/7** looking for exposed SSH ports.  
Weak configurations like **root login** and **password authentication** make servers an easy target.  

Common attack vectors:  
- 🔑 **Brute-force attacks** on passwords  
- 🕵️ **Exploiting default settings** (root login enabled, port 22 open)  
- 🧑‍💻 **Credential theft** via phishing or insecure storage  
- 🚪 **Privilege escalation** after initial access  

👉 Lesson: **SSH is secure by design, insecure by default.**  
You need to harden it for production.  

---

## 🛡️ SSH Best Practices  

### 1️⃣ Disable Root Login  
Root = all-powerful → also the most attacked.  

Edit `/etc/ssh/sshd_config`:  
```bash
PermitRootLogin no
✅ Use a normal user with sudo privileges instead.

2️⃣ Use Key-Based Authentication (Ditch Passwords)
Passwords = weak, guessable, brute-forced.
SSH keys = strong, cryptographically secure.

Generate a modern key pair:
ssh-keygen -t ed25519 -C "your_email@example.com"

Copy it securely:
ssh-copy-id user@server_ip

Disable password login in /etc/ssh/sshd_config:
PasswordAuthentication no
✅ Stronger, safer, and faster authentication.

3️⃣ Restrict Access by IP
Limit which IPs/users can connect:
AllowUsers devops@192.168.1.* sre@203.0.113.45
Or apply firewall rules with UFW/iptables.
✅ Reduces the attack surface.

4️⃣ Change Default SSH Port
Default 22 is noisy and heavily scanned.
Switch to a non-standard port:
Port 2222
⚠️ Not a silver bullet — but reduces automated attacks.

5️⃣ Enable Two-Factor Authentication (2FA)
Add an extra shield with OTP-based 2FA (e.g., Google Authenticator, Duo).
Configure via PAM (Pluggable Authentication Modules).

✅ Even if a private key leaks, attackers need your OTP.

6️⃣ Use SSH Config File for Efficiency
Define server shortcuts in ~/.ssh/config:
Host myserver
    HostName 192.168.1.10
    User ubuntu
    Port 2222
    IdentityFile ~/.ssh/id_ed25519

Now connect with:
ssh myserver
✅ No more remembering long commands.

7️⃣ Disable Empty or Weak Accounts
Check for accounts with empty passwords:
cat /etc/shadow | awk -F: '($2==""){print $1}'

List all users:
cat /etc/passwd
✅ Remove unused accounts immediately.

8️⃣ Monitor & Audit SSH Logs
Track failed logins:

Ubuntu/Debian → /var/log/auth.log

CentOS/RHEL → /var/log/secure

Block brute-force IPs automatically with Fail2Ban.

✅ Early detection of suspicious activity.

💡 Pro Tips & Tricks
🔑 Use Ed25519 keys (better than RSA).

🔄 Rotate SSH keys regularly.

🛡️ Use ssh-agent to manage keys securely.

🛠️ Automate hardening with Ansible / Puppet / Chef.

🧭 For enterprises → consider HashiCorp Vault or AWS SSM Session Manager to avoid direct SSH.

✅ Key Takeaways
SSH is powerful — but only if hardened properly.
To secure your infrastructure:

✔️ Disable root login
✔️ Use key-based authentication
✔️ Restrict by IP + change port
✔️ Enable 2FA for extra safety
✔️ Monitor & audit logs regularly

📌 Quick Checklist
 Root login disabled

 Password login disabled

 SSH keys enforced (Ed25519)

 Non-standard port configured

 Fail2Ban installed

 Users & accounts audited

 Logs monitored regularly

 2FA configured

🤝 Contribute
This guide is part of my DevOps Learning Series.
PRs and suggestions are welcome! 🚀

📚 References
OpenSSH Security Best Practices

Linux SSH Hardening Guide

Fail2Ban Documentation
