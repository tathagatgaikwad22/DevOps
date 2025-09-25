# 🛡️ SELinux & AppArmor Basics: A Practical Guide  

Security in Linux isn’t just about **file permissions** or **firewalls**. When services are compromised, attackers can often move laterally or escalate privileges.  

This is where **Mandatory Access Control (MAC)** systems like **SELinux** and **AppArmor** provide an **extra layer of defense** by restricting what processes *can* and *cannot* do.  

---

## 🔎 What Are SELinux & AppArmor?  

### **SELinux (Security-Enhanced Linux)**  
- Developed by the NSA, integrated into the Linux kernel.  
- Works on the principle of **labels (security contexts)**.  
- Every file, process, port, and resource has a label.  
- Policies define interactions between these labels.  

📌 Example:  
A web server (`httpd_t` context) cannot read a user’s SSH keys (`ssh_home_t`) even if file permissions allow it.  

---

### **AppArmor**  
- Developed by SUSE, widely used in Ubuntu/Debian.  
- Works with **profiles per application**.  
- Profiles define what an executable can read, write, or execute.  

📌 Example:  
An `nginx` profile can limit it to `/var/www/html`, blocking it from accessing `/etc/` even if permissions allow.  

---

## 📊 SELinux vs AppArmor  

| Feature           | SELinux                          | AppArmor                     |
|-------------------|----------------------------------|------------------------------|
| Enforcement Model | Labels on files & processes      | Profiles for applications    |
| Granularity       | Fine-grained                     | Simpler, less granular       |
| Complexity        | Steeper learning curve           | Easier to adopt              |
| Commonly Used In  | RHEL, CentOS, Fedora             | Ubuntu, Debian, SUSE         |

---

## ✅ Best Practices  

1. **Start Small**  
   - SELinux → Begin in *Permissive Mode*:  
     ```bash
     setenforce 0
     ```  
   - AppArmor → Use `complain` mode before enforcing.  

2. **Use Targeted Policies**  
   - Restrict only critical services (e.g., database, web server).  

3. **Audit Logs Regularly**  
   - SELinux logs: `/var/log/audit/audit.log`  
   - AppArmor logs: `/var/log/syslog` or `dmesg`  

4. **Update Policies/Profiles**  
   - Applications evolve → so should your security profiles.  

5. **Don’t Disable Blindly**  
   - Refine policies instead of turning them off.  

---

## ⚡ Tips & Tricks  

### 🔹 SELinux Commands  

Check status:  
```bash
getenforce

Troubleshoot denials:
ausearch -m avc -ts recent
sealert -a /var/log/audit/audit.log

Switch modes quickly:
setenforce 0   # Permissive
setenforce 1   # Enforcing

🔹 AppArmor Commands
List active profiles:
aa-status

Switch to complain mode:
aa-complain /etc/apparmor.d/usr.bin.nginx

Generate new profile interactively:
aa-genprof <application>

🧩 Real-World Scenario
🔐 Suppose your MySQL server is compromised via SQL injection.

Without MAC: Attacker may read /etc/passwd or modify system files.

With SELinux/AppArmor:

SELinux restricts MySQL to only its database files.

AppArmor confines MySQL to predefined directories.

✅ Result: Attack impact is minimized.

💡 Pro Tips for DevOps & Cloud Engineers
Containers: Both SELinux and AppArmor integrate with Docker & Kubernetes. Always enable them in production clusters.

Automation: Use Ansible/Puppet to deploy policies across environments.

Learning Curve: AppArmor is beginner-friendly, SELinux offers fine-grained enterprise control.

🎯 Conclusion
SELinux and AppArmor are not optional add-ons—they are key to defense-in-depth in modern infrastructure.

Instead of disabling them when things break, take time to analyze logs, tune policies, and enforce security.


👨‍💻 Maintained by Tathagat Gaikwad
📢 Contributions & suggestions are welcome!

#Linux #DevOps #Security #SELinux #AppArmor #SysAdmin



