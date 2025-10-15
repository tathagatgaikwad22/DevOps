
# 🧠 Mastering Git: How to Squash Commits into One (With Best Practices, Tips & Tricks)

If you’ve ever made multiple small commits like `fix typo`, `update readme`, or `final fix 😅`, you’re not alone.  
Before merging your branch, you should **squash commits** to keep your history clean and professional.  

---

## 💡 What Does “Squash Commits” Mean?

**Squashing** means **combining multiple commits into a single commit**.  
This creates a simpler and more readable commit history.

### Example:

**Before Squash:**
```
commit a12b4c: Added API route
commit c34d8f: Fixed typo in response
commit f78d9a: Updated comments
commit b90e1c: Updated README
```

**After Squash:**
```
commit e23a1b: Added API route with documentation
```

---

## 🎯 Why Squash Commits?

✅ Clean, easy-to-read history  
✅ Professional pull requests  
✅ Faster debugging and code review  
✅ Improves CI/CD visibility  

> “Squashing turns a cluttered commit timeline into a meaningful story.”

---

## ⚙️ Step-by-Step: How to Squash Commits

### 🪜 Method 1: Interactive Rebase (Local Squash)

```bash
git rebase -i HEAD~N
```
*(Replace N with the number of commits to squash)*

1. Git opens a list of recent commits.  
2. Keep the first as `pick`, change others to `squash` or `s`.  
3. Save and close the editor.  
4. Edit the combined commit message.  
5. Push changes:

```bash
git push origin branch-name --force-with-lease
```

> 💡 Use `--force-with-lease` for safety to avoid overwriting others’ work.

---

### 🪜 Method 2: Squash and Merge (GitHub / GitLab)

If you use GitHub or GitLab UI:

1. Open the Pull Request.  
2. Choose **“Squash and Merge”** option.  
3. Provide a single, clear commit message.  

This merges all commits in one clean step.

---

## 🧩 Best Practices for Squashing Commits

1. **Squash before merging** – keep your main branch clean.  
2. **Avoid squashing shared branches** – prevents history rewrite issues.  
3. **Write descriptive messages** – summarize purpose, not process.  
4. **Review before squash** – ensure tests and code checks pass.  
5. **Automate with aliases** – make squashing faster:

```bash
git config --global alias.squash '!f(){ git rebase -i HEAD~$1; }; f'
```

---

## 💡 Pro Tips and Tricks

🔥 Use `git log --oneline` to see commits before squashing.  
🔥 Combine with [Conventional Commits](https://www.conventionalcommits.org/) for structured messages.  
🔥 If needed, undo squash using:

```bash
git reflog
git reset --hard <commit_hash>
```

🔥 Use pre-push hooks to remind yourself to squash.  

---

## 🧠 Real-World Example

Feature branch: `feature/user-auth`  
Commits:
- Add login logic  
- Fix token issue  
- Update UI  
- Fix typo  
- Add logout feature  

After squash:
```
feat: implement user authentication and logout functionality
```

> Reviewers now see one clear, meaningful commit.

---

## 🧭 Common Mistakes to Avoid

🚫 Squashing after merging into main  
🚫 Forgetting to pull before rebase  
🚫 Using `--force` unsafely  
🚫 Poor commit messages  

---

## 🏁 Conclusion

> ✨ “A clean commit history reflects a disciplined developer.” ✨

Squashing makes your repository more maintainable, your reviews smoother, and your team collaboration more efficient.

---

### 📚 Quick Summary

| Step | Command / Action | Purpose |
|------|------------------|----------|
| Check commits | `git log --oneline` | Identify commits to squash |
| Start rebase | `git rebase -i HEAD~N` | Choose commits to squash |
| Merge messages | Edit & save | Combine commit messages |
| Push safely | `git push --force-with-lease` | Update remote branch |
| Merge | “Squash and Merge” | Keep history clean |

---

## 🔖 Tags

#Git #GitHub #GitLab #DevOps #VersionControl #CleanCode #BestPractices #SoftwareEngineering #GitRebase
