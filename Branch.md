# 🌿 Git Branching & Merging Practice

This repository is focused on **learning Git branching strategies**.  
We will cover creating, switching, merging, deleting, and resolving conflicts in branches.  

---

## 🔧 Setup

```bash
git init
echo "# Git Branch Practice 🌿" > README.md
git add README.md
git commit -m "chore: initial commit"
````

---

## 🪜 Step 1: Create and Switch Branch

```bash
# create new branch
git branch feature/login

# switch branch
git checkout feature/login

# shortcut (create + switch)
git checkout -b feature/signup
```

---

## 📂 Step 2: Add Work in Branch

```bash
echo "Login feature started" > login.txt
git add login.txt
git commit -m "feat: add login feature file"
```

---

## 🔄 Step 3: Push Branch to Remote

```bash
git push -u origin feature/login
```

---

## 🌲 Step 4: View Branches

```bash
git branch          # local branches
git branch -r       # remote branches
git branch -a       # all branches
```

---

## 🔀 Step 5: Merge Branch into Main

```bash
# go to main branch
git checkout main
git pull origin main

# merge feature branch
git merge feature/login

# push updates
git push origin main
```

---

## ⚔️ Step 6: Resolve Merge Conflicts

If two branches edit the same line:

```bash
git checkout main
git merge feature/signup
```

Conflict example in file:

```diff
<<<<<<< HEAD
main branch content
=======
feature branch content
>>>>>>> feature/signup
```

Resolve manually, then:

```bash
git add conflicted-file.txt
git commit -m "fix: resolve merge conflict"
```

---

## 🗑️ Step 7: Delete Branch

```bash
# delete local branch
git branch -d feature/login

# force delete
git branch -D feature/login

# delete remote branch
git push origin --delete feature/login
```

---

## 📦 Step 8: Rebase Branch (Alternative to Merge)

```bash
git checkout feature/signup
git rebase main
```

> ⚠️ Rebase rewrites history, use carefully on shared branches.

---

## 🚀 Step 9: Stash Work (Before Switching Branches)

```bash
git stash save "work in progress"
git stash list
git stash pop
```

---

## 🌐 Step 10: Branch Naming Conventions

* `feature/*` → new features
* `bugfix/*` → bug fixes
* `hotfix/*` → urgent fixes
* `release/*` → release prep
* `main` → stable production branch
* `develop` → active development branch

---

## ✅ Practice Checklist

* [ ] Create & switch branches
* [ ] Add commits in feature branches
* [ ] Push branch to GitHub
* [ ] Merge feature → main
* [ ] Handle merge conflicts
* [ ] Delete old branches
* [ ] Try rebasing
* [ ] Use stash for temporary work

---

## 🔥 Pro Tips

* Use `git log --oneline --graph --all` to see branch structure
* Always `git pull origin main` before merging to reduce conflicts
* Work on separate branches instead of directly on `main`

