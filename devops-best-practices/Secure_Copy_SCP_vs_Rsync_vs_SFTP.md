# 🔐 Secure Copy (SCP) vs Rsync vs SFTP

A detailed guide comparing **SCP**, **Rsync**, and **SFTP** for secure file transfer and synchronization.  
This guide is written for **DevOps Engineers, SREs, SysAdmins, and Cloud professionals**.

---

## 📌 1. SCP (Secure Copy Protocol)

**What is it?**  
SCP is the simplest tool for securely copying files between hosts over SSH. Think of it as `cp` but across machines.

**How it works:**  
- Relies on SSH for authentication and encryption.  
- Transfers files in one go (no resume support).

**Use Cases:**  
- Quick, one-time file transfers.  
- Copying files between local and remote servers.  

**Examples:**
```bash
# Copy a file from local to remote
scp file.txt user@server:/home/user/

# Copy directory recursively
scp -r project/ user@server:/var/www/

# Enable compression for large transfers
scp -C largefile.tar.gz user@server:/backup/
Best Practices:

Use -C for compression when working with large files.

Always use absolute paths to avoid mistakes.

Configure SSH keys for automation instead of passwords.

📌 2. Rsync (Remote Sync)
What is it?
Rsync is a fast and versatile file synchronization tool. It copies only the differences between source and destination, saving time and bandwidth.

How it works:

Uses checksums/timestamps to detect changes.

Transfers only modified parts of files (incremental updates).

Use Cases:

Automated backups.

Deployments (sync only changed files).

Syncing large directories efficiently.

Examples:

# Sync directory to remote server
rsync -avz project/ user@server:/var/www/project/

# Show progress and resume partial transfers
rsync -avz --progress --partial project/ user@server:/var/www/project/

# Mirror a directory (delete extra files on destination)
rsync -avz --delete project/ user@server:/var/www/project/
Best Practices:

Use -a for archive mode (preserves permissions, symlinks, metadata).

Add --delete to maintain an exact mirror.

Automate with cron for scheduled backups.

Control bandwidth with --bwlimit=1000.

📌 3. SFTP (SSH File Transfer Protocol)
What is it?
SFTP is an interactive file transfer protocol built on SSH. Unlike SCP or Rsync, it supports browsing, directory management, and resuming transfers.

How it works:

Starts an interactive session similar to FTP but secured with SSH.

Supports advanced file operations (rename, delete, list, resume).

Use Cases:

Manual file management on remote servers.

Automated scripted transfers with batch files.

Transfers requiring resume functionality.

Examples:

# Start interactive session
sftp user@server

# Inside session
sftp> put localfile.txt
sftp> get remotefile.log
sftp> ls
sftp> exit

Batch Automation:
# batch.txt
put localfile.txt
get remotefile.log
exit

# Run batch file
sftp -b batch.txt user@server
Best Practices:

Use batch mode for automation.

Secure with SSH keys (no passwords in scripts).

Great for manual exploration when unsure about remote directory structure.

🚀 Best Practices (All Tools)
Always use SSH keys instead of passwords for security and automation.

Enable compression (-C for SCP, -z for Rsync) for large text files.

Use Rsync for production backups (saves bandwidth & time).

Use SCP for quick, one-time transfers.

Use SFTP for interactive/manual file management.

Combine Rsync with cron jobs for automated backups.

Test commands with --dry-run in Rsync before running live.

🔥 Final Thoughts
SCP → Great for quick, simple transfers.

Rsync → Best for incremental backups and efficient sync.

SFTP → Ideal for interactive/manual file operations.

👉 Knowing when to use which makes you more effective as a DevOps/SRE/Cloud Engineer.

🌟 Contributions
Feel free to fork this repo, add examples, and submit a PR with improvements!
