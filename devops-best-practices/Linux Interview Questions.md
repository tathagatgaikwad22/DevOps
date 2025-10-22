# 馃惂 10 Must-Know Linux Interview Questions and Answers

This guide covers the **top 10 Linux interview questions** every **DevOps**, **Cloud**, or **System Administrator** should know 鈥� with explanations, examples, and pro tips.  

---

## 馃敼 1. What is the difference between a hard link and a soft link (symbolic link)?

| Type | Description | Command Example |
|------|--------------|-----------------|
| **Hard Link** | Points directly to the inode of a file. Even if the original file is deleted, the link still works. | `ln file.txt hardlink.txt` |
| **Soft Link (Symbolic)** | Points to the file path, not the inode. If the original file is deleted, the link breaks. | `ln -s file.txt softlink.txt` |

**Pro Tip:**  
Use **hard links** for data backup consistency and **soft links** for shortcuts.

---

## 馃敼 2. How do you check disk usage and available space?

| Command | Description |
|----------|--------------|
| `df -h` | Shows disk space in human-readable format. |
| `du -sh *` | Displays size of each directory/file in the current folder. |

**Example:**
```bash
df -h
du -sh /var/log
```

---

## 馃敼 3. What鈥檚 the difference between `cron` and `at` commands?

| Command | Purpose | Use Case |
|----------|----------|----------|
| `cron` | Schedule recurring tasks. | Backup every day at midnight. |
| `at` | Schedule one-time tasks. | Run a script tomorrow at 5 PM. |

**Examples:**
```bash
crontab -e
# Add: 0 0 * * * /path/to/script.sh

at 17:00 tomorrow
# at> /path/to/script.sh
```

---

## 馃敼 4. How do you find which process is using a specific port?

**Command:**
```bash
sudo lsof -i :8080
sudo netstat -tulnp | grep 8080
sudo ss -tuln | grep 8080
```

**Pro Tip:**  
Use `ss` over `netstat` 鈥� it鈥檚 faster and more modern.

---

## 馃敼 5. Difference between `sudo` and `su`

| Command | Description |
|----------|--------------|
| `sudo` | Executes a command as another user (usually root) temporarily. | `sudo apt update` |
| `su` | Switches to another user account (default: root) until exit. | `su -` |

**Pro Tip:**  
Use `sudo` for single commands 鈥� safer than full root sessions.

---

## 馃敼 6. Difference between `grep`, `egrep`, and `fgrep`

| Command | Description |
|----------|--------------|
| `grep` | Basic text search using regex. |
| `egrep` | Extended grep (supports more regex patterns). |
| `fgrep` | Fixed grep (searches exact string, no regex). |

**Example:**
```bash
grep "error" logfile.txt
egrep "error|fail" logfile.txt
fgrep "error?" logfile.txt
```

---

## 馃敼 7. How can you check memory and CPU usage?

| Command | Description |
|----------|--------------|
| `top` / `htop` | Real-time process and resource usage. |
| `free -h` | Shows memory usage in human-readable format. |
| `vmstat` | Reports memory, processes, I/O, and CPU stats. |

**Example:**
```bash
top
free -h
```

---

## 馃敼 8. What are runlevels (or systemd targets)?

| Runlevel | Meaning | systemd Target |
|-----------|----------|----------------|
| 0 | Halt | `poweroff.target` |
| 1 | Single-user mode | `rescue.target` |
| 3 | Multi-user (no GUI) | `multi-user.target` |
| 5 | Multi-user (with GUI) | `graphical.target` |
| 6 | Reboot | `reboot.target` |

**Command:**
```bash
systemctl get-default
sudo systemctl set-default multi-user.target
```

---

## 馃敼 9. How do you troubleshoot a service that fails to start?

**Steps:**
1. Check the service status:
   ```bash
   systemctl status nginx
   ```
2. View logs for details:
   ```bash
   journalctl -xe
   ```
3. Check configuration syntax:
   ```bash
   nginx -t
   ```
4. Restart and verify:
   ```bash
   sudo systemctl restart nginx
   sudo systemctl enable nginx
   ```

**Pro Tip:**  
Always inspect logs under `/var/log/` 鈥� they鈥檙e your best friend during troubleshooting.

---

## 馃敼 10. Explain the difference between `/etc/passwd` and `/etc/shadow` files.

| File | Description | Access |
|------|--------------|---------|
| `/etc/passwd` | Stores user information (username, UID, shell, etc.). | Readable by all users. |
| `/etc/shadow` | Stores encrypted user passwords and expiry info. | Readable only by root. |

**Example:**
```bash
cat /etc/passwd | head
sudo cat /etc/shadow | head
```

---

## 馃 Bonus Tips for Linux Interviews

鉁� Practice basic file, process, and user management.  
鉁� Understand permissions (`chmod`, `chown`, `umask`).  
鉁� Learn to use `systemctl`, `journalctl`, and `grep` effectively.  
鉁� Use real-world examples from your projects (DevOps, CI/CD, or Cloud).  

---

### 馃専 Author: Anand Gaikwad  
馃捈 *Aspiring DevOps Engineer | #90DaysOfDevOps Challenge*  
馃敆 Connect on [LinkedIn](https://www.linkedin.com/in/anandgaikwad/)  

---

**猸� If you found this helpful, give this repo a star and share with your peers!**  
#Linux #DevOps #InterviewQuestions #CloudComputing #SysAdmin #Learning
