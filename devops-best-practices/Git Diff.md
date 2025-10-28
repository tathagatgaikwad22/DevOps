# 🔍 Git Diff — Advanced Usage, Theory, Best Practices & Pro Tips

`git diff` is one of Git’s most powerful commands — it reveals exactly what changed between commits, branches, or your working tree and the index. This guide will take you from basic uses to advanced workflows, show practical examples, and share best practices and tricks used by professionals.

---

## 📘 Table of Contents
1. [Theory: What `git diff` does](#theory-what-git-diff-does)
2. [Common and Advanced Usage](#common-and-advanced-usage)
3. [Options & Flags Cheat Sheet](#options--flags-cheat-sheet)
4. [Practical Examples](#practical-examples)
5. [Best Practices](#best-practices)
6. [Pro Tips & Tricks](#pro-tips--tricks)
7. [Integrations & Automation](#integrations--automation)
8. [Quick Reference Table](#quick-reference-table)
9. [Further Reading](#further-reading)

---

## 🧠 Theory — What `git diff` Does

At a high level, `git diff` computes and displays the *difference* between two Git object trees. These trees can be:

- Your working directory vs. the index (unstaged changes): `git diff`
- The index vs. the last commit (staged changes): `git diff --cached`
- Two commits, tags, or branches: `git diff <commit1> <commit2>`
- Any combination of refs, files, and paths

Git uses a three-way model (working tree, index/staging area, and HEAD). `git diff` shows the “delta” between any two states in that model.

---

## ⚙️ Common and Advanced Usage

### 1. Compare working directory vs last commit (unstaged)
```bash
git diff
```

### 2. Compare staged vs last commit (what will be committed)
```bash
git diff --cached
```

### 3. Compare two branches
```bash
git diff main feature/login
```

### 4. Compare two commits
```bash
git diff 3f1a2b7 4e9c2a6
```

### 5. Compare a single file between commits or branches
```bash
git diff main..feature -- src/app.py
git diff 3f1a2b7..4e9c2a6 -- src/app.py
```

### 6. Ignore whitespace changes
```bash
git diff -w
git diff --ignore-all-space
```

### 7. Show stats only
```bash
git diff --stat
```

### 8. Word-level diff (good for docs)
```bash
git diff --color-words
```

### 9. Create a patch file
```bash
git diff > changes.patch
```

### 10. Visual diff using external tool
```bash
git difftool
# or specify tool
git difftool --tool=meld
```

---

## 🧾 Options & Flags — Cheat Sheet

- `--cached` : show staged changes
- `--staged` : same as `--cached`
- `--name-only` : show changed filenames only
- `--name-status` : show filenames with change status (A/M/D)
- `--stat` : concise summary of changes
- `-w` / `--ignore-all-space` : ignore whitespace
- `--color-words` : word-level inline diff
- `--patch` / `-p` : show patch format (default)
- `--unified=<n>` : context lines in unified diff
- `--word-diff` : alternative word diff format
- `--relative` : limit paths to relative
- `--no-index` : diff two paths outside of git repo

---

## 🧩 Practical Examples

**A. Check what you're about to commit**
```bash
git add src/
git diff --cached   # review staged changes
```

**B. Review differences before merging**
```bash
git fetch origin
git diff origin/main..feature-branch --stat
```

**C. Ignore formatting-only commits while reviewing**
```bash
git diff -w main..feature-branch
```

**D. Show concise filename changes**
```bash
git diff --name-only HEAD~5 HEAD
```

**E. Create patch to send as email or apply elsewhere**
```bash
git diff HEAD~1 HEAD > fix.patch
# apply with:
git apply fix.patch
```

---

## ✅ Best Practices

- **Always run `git diff` before committing.** It avoids accidental changes and ensures commit granularity.
- **Use `git diff --cached` to review what will be committed.**
- **Prefer focused diffs.** Limit scope with `-- <path>` to avoid noise in large repos.
- **Use `-w` during reviews when only formatting changes are expected.**
- **Combine diffs with `git log -p`** to review changes over time.
- **Use aliases** for your most common diff configurations to save time.

Example alias:
```bash
git config --global alias.df "diff --color-words"
```

---

## ✨ Pro Tips & Tricks

- **Side-by-side visual diffs:** Configure your `difftool` (`git config --global diff.tool meld`) and use `git difftool` for a two-panel view.
- **Partial commits & hunk staging:** Use `git add -p` or interactive staging to stage only specific hunks after inspecting with `git diff`.
- **Detect file renames:** Add `-M` to detect renames during diffs `git diff -M`.
- **Use `--name-status`** to get type of change (Added/Modified/Deleted) quickly.
- **Combine with `grep` to find changes in specific code areas:**  
  ```bash
  git diff main..feature | grep -n "TODO"
  ```
- **Diff from remote without checking out:**  
  ```bash
  git fetch origin
  git diff origin/main..origin/branch
  ```

---

## 🔁 Integrations & Automation

- **CI/CD conditional runs:** Use `git diff --name-only` to run tests only for affected modules.
  ```bash
  CHANGED_FILES=$(git diff --name-only origin/main...HEAD)
  if echo "$CHANGED_FILES" | grep -q "serviceA/"; then
    # run serviceA tests
  fi
  ```
- **Pre-commit hooks:** Add `git diff` checks in pre-commit to fail commits if large or unsafe diffs occur.
- **Code review bots:** Many bots analyze `git diff` output to enforce style, security, or coverage checks.

---

## 🧾 Quick Reference Table

| Task | Command |
|------|---------|
| Show unstaged changes | `git diff` |
| Show staged changes | `git diff --cached` |
| Show files changed between two refs | `git diff --name-only ref1 ref2` |
| Show stats summary | `git diff --stat ref1 ref2` |
| Ignore whitespace | `git diff -w` |
| Word diff | `git diff --color-words` |
| Create patch | `git diff > changes.patch` |

---

## 📚 Further Reading

- `git-diff(1)` in the Git manual: https://git-scm.com/docs/git-diff  
- Pro Git Book — Chapter on Git tools: https://git-scm.com/book/en/v2/Git-Tools-Diffing  
- Articles on `git difftool` and `git add -p`

---

## 🚀 Closing Thought

`git diff` is not just a command — it's a lens into your codebase and an essential part of safe, professional development. Master it to avoid surprises, improve reviews, and automate smarter workflows.

---

**Tags:** `Git` `DevOps` `Version Control` `git-diff` `Best Practices`
