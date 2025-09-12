# 🔐 Understanding `/etc/passwd` and `/etc/shadow` in Linux

This repository contains a detailed guide on two of the most important files in Linux user management and authentication: `/etc/passwd` and `/etc/shadow`. These files form the foundation of how users are identified and authenticated on a Linux system.

---

## 📖 `/etc/passwd` – User Identity Database

Originally, `/etc/passwd` stored both usernames and plaintext passwords. For security, Linux now uses it only for **user account metadata**.

- **Permissions:** `644` (world-readable).
- **Purpose:** Provides information needed by processes to resolve user IDs.

**Structure:**
```text
username : placeholder : UID : GID : comment : home_directory : shell
```

**Example:**
```text
sam:x:1001:1001:Sam Lee:/home/sam:/bin/bash
```

**Field breakdown:**
- `username` → login name
- `x` → placeholder (password moved to `/etc/shadow`)
- `UID` → user ID
- `GID` → group ID
- `comment` → optional description
- `home_directory` → user’s home folder
- `shell` → default login shell

📌 **Theory:** `/etc/passwd` is world-readable because many programs need to translate UID ↔ username. Without it, your system breaks.

---

## 🔐 `/etc/shadow` – Authentication Vault

The Shadow Password Suite was introduced to move sensitive password hashes out of `/etc/passwd` and restrict access.

- **Permissions:** `600` (root only).
- **Purpose:** Stores **hashed passwords** and **password aging information**.

**Structure:**
```text
username : hashed_password : last_change : min_age : max_age : warn : inactive : expire : reserved
```

**Example:**
```text
sam:$6$Qk3n$ENCRYPTEDHASH:19500:0:99999:7:::
```

**Field breakdown:**
- `username` → login name
- `hashed_password` → encrypted password hash (`$6$` = SHA-512)
- `last_change` → days since Jan 1, 1970
- `min_age` → minimum days before password can be changed
- `max_age` → maximum days before password expires
- `warn` → days before expiry warning
- `inactive` → days after expiry before account is locked
- `expire` → account expiration date

📌 **Theory:** Separating `/etc/shadow` from `/etc/passwd` dramatically improved Linux security.

---

## 🛡️ Best Practices

✅ **File Permissions:**
- `/etc/passwd` → `644`, owned by `root:root`
- `/etc/shadow` → `600`, owned by `root:root`

✅ **Strong Hashes:**
- Use SHA-512 (default in modern distros).
- Avoid outdated MD5 or DES hashes.

✅ **Password Policies:**
- Enforce aging with `chage`.
- Use PAM for complexity requirements.

✅ **Account Management:**
- Lock unused accounts → `usermod -L username`
- Disable login for service accounts → `usermod -s /usr/sbin/nologin username`
- Expire accounts → `chage -E 2025-12-31 username`

✅ **Better Authentication:**
- Prefer **SSH keys** or MFA instead of passwords.
- Integrate with LDAP/SSO in enterprise setups.

---

## ⚡ Useful Commands & Tricks

🔍 Check password status:
```bash
passwd -S username
```

📅 View password aging rules:
```bash
chage -l username
```

📝 Safely edit passwd/shadow:
```bash
vipw       # edits /etc/passwd safely
vipw -s    # edits /etc/shadow safely
```

🔒 Find accounts with no passwords:
```bash
awk -F: '($2=="!")||($2=="*"){print $1}' /etc/shadow
```

🚫 Disable shell access for system accounts:
```bash
usermod -s /usr/sbin/nologin username
```

---

## 🎯 Key Takeaways

- `/etc/passwd` = **Identity & metadata**
- `/etc/shadow` = **Authentication & policies**

Together, they define how Linux handles user access. A solid understanding of these files is crucial for any **SysAdmin, DevOps Engineer, or SRE**.

---

### 📌 Contribution
Feel free to fork this repo and add more best practices or security hardening tips for Linux user management.

#Linux #SysAdmin #DevOps #SRE #Security
