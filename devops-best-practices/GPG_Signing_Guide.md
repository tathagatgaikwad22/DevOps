# 🔐 Signing Git Commits with GPG — Complete Guide, Best Practices & Pro Tips

## 🧠 What is GPG Signing in Git?
**GPG (GNU Privacy Guard)** is a tool that uses cryptographic keys to verify identity and integrity.

When you sign a Git commit:
- Git uses your **private key** to generate a unique digital signature.
- Anyone with your **public key** can verify that you made that commit.

It’s like putting your **digital fingerprint** on your code.

> GPG signing ensures your commits are authentic, unaltered, and truly yours.

---

## 🛡️ Why Sign Commits?

In collaborative or open-source environments, unsigned commits can pose risks — anyone could impersonate your username and email.

Signing your commits solves that.

### Benefits
✅ **Authenticity** – Confirms the commit was made by you.  
✅ **Integrity** – Ensures code wasn’t modified after signing.  
✅ **Trust** – Builds credibility within teams or open-source projects.  
✅ **Security** – Protects against impersonation or supply chain attacks.  
✅ **Style points** – You get the cool green “Verified” badge 😎

---

## ⚙️ How GPG Commit Signing Works

GPG uses **asymmetric encryption** (two keys):
- A **private key** (kept secret)
- A **public key** (shared for verification)

When you commit:
1. Git hashes your commit data.
2. GPG signs the hash with your private key.
3. GitHub verifies it with your public key.

If it matches → ✅ “Verified” appears next to your commit.

---

## 🧩 Step-by-Step Setup Guide

### Step 1: Install GPG

**Linux / Mac:**
```bash
sudo apt install gnupg
```

**Windows:**
Download and install [Gpg4win](https://gpg4win.org)

---

### Step 2: Generate a GPG Key
```bash
gpg --full-generate-key
```
Choose:
- Key type: RSA and RSA (option 1)
- Key size: 4096
- Expiration: 1y (you can renew)
- Name & Email: same as your GitHub email

---

### Step 3: List Your Key
```bash
gpg --list-secret-keys --keyid-format=long
```
Example output:
```
sec   rsa4096/ABCD1234EFGH5678 2025-10-17 [SC]
```

---

### Step 4: Export Your Public Key
```bash
gpg --armor --export ABCD1234EFGH5678
```
Copy everything between:
```
-----BEGIN PGP PUBLIC KEY BLOCK-----
...
-----END PGP PUBLIC KEY BLOCK-----
```

---

### Step 5: Add Key to GitHub
Go to:
**GitHub → Settings → SSH and GPG Keys → New GPG Key**  
Paste the key and click **Save**.

---

### Step 6: Configure Git to Use GPG
```bash
git config --global user.signingkey ABCD1234EFGH5678
git config --global commit.gpgsign true
```

---

### Step 7: Test Your Signed Commit
```bash
git commit -S -m "My first signed commit"
```
Push it → You’ll see ✅ **Verified** on GitHub!

---

## 🏷️ Sign Tags Too!
```bash
git tag -s v1.0.0 -m "Signed release v1.0.0"
```

---

## 🧠 Understanding GPG Keys

| Type | Description |
|------|--------------|
| **Public Key** | Shared with others to verify your commits |
| **Private Key** | Kept secret, used to sign your commits |
| **Key ID** | Short identifier for your GPG key |
| **Fingerprint** | Full unique identifier (hash) of your key |

---

## ✅ Best Practices

### 🔐 1. Use Strong Keys
Use **RSA 4096** or **ECC 25519**.

### 🔒 2. Protect Your Private Key
Store it securely and use a strong passphrase.

### 🔁 3. Rotate Keys Regularly
Set expiration and renew every year.

### 🌍 4. Publish Public Keys
```bash
gpg --send-keys <KEY_ID>
```

### 🧑‍💻 5. Automate in CI/CD
Import GPG keys securely in pipelines for verified builds.

---

## ⚡ Pro Tips & Tricks

💡 **Tip 1:** Sign Only Specific Commits  
```bash
git commit -S -m "Signed commit only"
```

💡 **Tip 2:** Use Project-Specific Keys  
```bash
git config user.signingkey <KEY_ID>
```

💡 **Tip 3:** Cache GPG Passphrase  
```bash
export GPG_TTY=$(tty)
```

💡 **Tip 4:** GitHub CLI Setup  
```bash
gh auth setup-gpg
```

💡 **Tip 5:** Verify Signature Validity  
```bash
git log --show-signature
```

---

## ⚖️ When to Use GPG Signing

✅ **Use When:**
- You work in open-source projects
- Security and traceability matter
- CI/CD pipelines handle production releases

🚫 **Skip When:**
- Solo personal projects or prototypes

---

## 🧭 Quick Summary

| Step | Command | Description |
|------|----------|-------------|
| 1 | `gpg --full-generate-key` | Generate GPG key |
| 2 | `gpg --list-secret-keys` | Get key ID |
| 3 | `gpg --armor --export <KEY>` | Copy public key |
| 4 | Add to GitHub | Verify identity |
| 5 | `git config --global commit.gpgsign true` | Enable signing |
| 6 | `git commit -S -m "msg"` | Sign commit |

---

## 🧩 Common Issues

❌ **Error:** gpg failed to sign data  
✅ **Fix:**  
```bash
export GPG_TTY=$(tty)
```

❌ **Error:** Commit shows “Unverified”  
✅ **Fix:** Ensure GitHub email matches GPG key email.

❌ **Error:** Repeated passphrase prompt  
✅ **Fix:** Use `gpg-agent` for caching.

---

## 💬 Final Thoughts

Signing Git commits isn’t just about security — it’s about **authenticity and professionalism**.  
It builds confidence and ensures your work is verifiable and trusted.

> “Unsigned commits say who wrote the code. Signed commits prove you did.”

---

## ✍️ Author
Written by **[Tathagat Gaikwad]**  
🔖 *#Git #GPG #DevOps #CyberSecurity #GitHub #VersionControl #OpenSource #90DaysOfDevOps*
