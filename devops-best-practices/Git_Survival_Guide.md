
# 🧭 Git Survival Guide — Cheat Sheet for Developers & DevOps Engineers

> “A developer who knows Git well never fears version control chaos.”

This **Git Survival Guide** is a complete, ready-to-use reference with **detailed theory, commands, best practices, tips, and tricks**.  
Perfect for your GitHub repository or quick reference during development.

---

## 🧠 What Is Git?

Git is a **distributed version control system (DVCS)** that tracks every change in your project.  
Each version of your project is stored as a *snapshot* (called a commit).

### 🔹 Git’s Core Concepts
- **Repository** → A directory where Git tracks files and history.  
- **Commit** → A snapshot of changes.  
- **Branch** → A pointer to a specific commit.  
- **Merge** → Combine changes from different branches.  
- **Rebase** → Replay commits from one branch onto another for a cleaner history.  

---

## 🧩 The Git Workflow

```
Working Directory → Staging Area → Repository
```

| Area | Description | Command Example |
|------|--------------|----------------|
| Working Directory | Where you modify files | `git status` |
| Staging Area | Prepare files to commit | `git add <file>` |
| Repository | Permanent storage for commits | `git commit -m "msg"` |

---

## ⚙️ Essential Git Commands

| Task | Command | Notes |
|------|----------|-------|
| Initialize repo | `git init` | Start version control |
| Clone repo | `git clone <url>` | Copy existing repo |
| Check status | `git status` | View modified/staged files |
| Stage files | `git add .` | Add all changes |
| Commit changes | `git commit -m "message"` | Save snapshot |
| Undo commit | `git reset --soft HEAD~1` | Keep changes staged |
| View history | `git log --oneline --graph` | Visualize branches |
| Create branch | `git checkout -b feature` | New feature branch |
| Merge branch | `git merge feature` | Combine code |
| Rebase branch | `git rebase main` | Clean history |
| Push changes | `git push origin main` | Upload to remote |
| Pull updates | `git pull origin main` | Get latest changes |
| Stash changes | `git stash` / `git stash pop` | Temporarily save work |

---

## ✅ Best Practices

1. **Commit Often, Commit Small**
   - Each commit = one logical change.
2. **Use Clear Messages**
   - Example: `fix: resolve login token issue`
3. **Protect Main Branch**
   - Use branch protection & PR reviews.
4. **Ignore Unnecessary Files**
   ```bash
   # .gitignore
   .env
   node_modules/
   *.log
   ```
5. **Always Pull Before Push**
   ```bash
   git pull origin main --rebase
   ```
6. **Use Feature Branches**
   ```bash
   git checkout -b feature/new-ui
   ```

---

## 💡 Pro Tips & Tricks

| Tip | Command | Use Case |
|-----|----------|----------|
| Recover lost commits | `git reflog` | Restore deleted commits |
| Clean commit history | `git rebase -i HEAD~5` | Squash or rename commits |
| Find who changed a line | `git blame <file>` | Track changes |
| Apply a specific commit | `git cherry-pick <hash>` | Copy commits |
| Inline diff | `git diff --color-words` | Highlight word changes |
| Save unfinished work | `git stash` | Temporary storage |

---

## 🔧 Git Aliases for Speed

```bash
git config --global alias.st status
git config --global alias.cm "commit -m"
git config --global alias.lg "log --oneline --graph --decorate --all"
```

Now you can run:
```bash
git st
git cm "Initial commit"
git lg
```

---

## 🚀 Integrating Git with DevOps

- **Automate builds:** Use CI/CD tools (Jenkins, GitHub Actions).  
- **Tag releases:**  
  ```bash
  git tag -a v1.0.0 -m "Stable release"
  git push origin v1.0.0
  ```
- **Pre-commit hooks:** Ensure code quality before commits.  
  ```bash
  # .git/hooks/pre-commit
  npm run lint
  ```

---

## 📚 Advanced Git Topics

- `git revert` vs `git reset`
- Managing submodules (`git submodule`)
- Using multiple worktrees (`git worktree`)
- Signed commits using GPG
- Partial staging (`git add -p`)

---

## 🧭 Git Survival Summary

| Area | Tip |
|------|-----|
| Workflow | Commit often, push regularly |
| Collaboration | Protect main branch |
| Cleanup | Rebase & squash commits |
| Recovery | Use `reflog` to restore |
| Automation | Pre-commit hooks & CI/CD |

---

## 💬 Final Thoughts

Git isn’t just about commands — it’s about *understanding change flow*.  
Once you know how Git works internally, you’ll code with confidence.

💡 *Break, fix, and learn. Every Git pro once lost a commit and came back stronger.*

---

**Author:** Tathagat Gaikwad  
**Tags:** `#Git` `#DevOps` `#VersionControl` `#CheatSheet` `#BestPractices`
