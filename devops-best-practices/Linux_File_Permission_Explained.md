# 🛡️ Linux File Permissions Explained — A Complete Guide

Managing file permissions is one of the most **essential Linux skills** every engineer must master. Permissions control who can **read, write, or execute** files, and misconfigured settings can lead to **security risks or broken applications**. 🚀

This guide is tailored for your **GitHub learning repo**, with **theory, best practices, examples, pro tips, and tricks**.

---

## 🔑 Understanding File Permissions

In Linux, every file and directory has **three types of permissions**:

* **Read (r)** → view contents of a file or list files in a directory
* **Write (w)** → modify contents of a file or add/remove files in a directory
* **Execute (x)** → run a file (if it’s a script or program) or access a directory

And they apply to **three categories of users**:

* **Owner (u)** → the user who owns the file
* **Group (g)** → users in the file’s group
* **Others (o)** → everyone else

👉 Example permission: `-rwxr-xr--`

* **Owner (u)** → `rwx` → read, write, execute
* **Group (g)** → `r-x` → read, execute
* **Others (o)** → `r--` → read only

---

## 📊 File Permission Representation

Permissions can be represented in **symbolic** or **numeric (octal)** form:

| Permission | Symbolic | Numeric |
| ---------- | -------- | ------- |
| rwx        | u=rwx    | 7       |
| rw-        | u=rw-    | 6       |
| r-x        | u=r-x    | 5       |
| r--        | u=r--    | 4       |
| -wx        | u=wx     | 3       |
| -w-        | u=w-     | 2       |
| --x        | u=x      | 1       |
| ---        | none     | 0       |

Example: `chmod 754 file.txt` →

* Owner → 7 (rwx)
* Group → 5 (r-x)
* Others → 4 (r--)

---

## ⚙️ Common Commands

### 1. Check permissions

```bash
ls -l
```

### 2. Change permissions

```bash
chmod 755 script.sh   # Numeric method
chmod u+x script.sh   # Symbolic method
```

### 3. Change ownership

```bash
chown user:group file.txt
```

### 4. Recursive permission change

```bash
chmod -R 644 /var/www/html
```

### 5. Default permissions (umask)

```bash
umask
```

---

## ✅ Best Practices

* 🔒 **Principle of least privilege** → Give only necessary permissions.
* 📂 **Directories usually need execute (x)** so users can traverse.
* 🚫 **Never use 777** unless absolutely required (everyone gets full rights).
* 📝 **Scripts should be 755** (executable by owner and readable by others).
* 🔑 **Configuration files** (like `/etc/passwd`) should be 644.

---

## 💡 Pro Tips & Tricks

* Use `stat file.txt` → for detailed permission + inode info.
* Use `groups <username>` → check user’s groups (affects group permissions).
* Add execute permission quickly:

  ```bash
  chmod +x script.sh
  ```
* Remove write access for others:

  ```bash
  chmod o-w file.txt
  ```
* Use ACLs for fine-grained control:

  ```bash
  setfacl -m u:john:rwx file.txt
  ```

---

## 🔍 Real-World Examples

1. **Web server files**

   ```bash
   chmod 644 /var/www/html/index.html
   chmod 755 /var/www/html/
   ```

   (Owner can edit, everyone else can only read)

2. **Private SSH key**

   ```bash
   chmod 600 ~/.ssh/id_rsa
   ```

   (Owner can read/write, no one else can access)

3. **Shared project directory**

   ```bash
   chmod 770 /project/team
   ```

   (Owner + group can access, others blocked)

---

## 🎯 Conclusion

File permissions are **the backbone of Linux security and collaboration**. With the right mix of **theory, best practices, and hands-on tips**, you can:

* Secure sensitive files
* Enable safe team collaboration
* Avoid costly misconfigurations

👨‍💻 Mastering Linux permissions isn’t optional—it’s a **superpower** every engineer must have.

---

⭐ If you liked this guide, don’t forget to **star** ⭐ this repo and share it with your DevOps/Linux peers!
