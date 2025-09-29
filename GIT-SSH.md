# 🔐 Git Practice with SSH (Step-by-Step)

This repository is created to **practice Git operations using SSH**.  
We will cover setup, file management, commits, branches, push/pull, and token-free authentication.  

---

## 🔧 Setup

```bash
# check git version
git --version

# configure global identity
git config --global user.name "Sahil Shaikh"
git config --global user.email "your_email@example.com"
````

---

## 🗝️ Step 1: Generate SSH Key

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

* Save default path: `~/.ssh/id_ed25519`
* Press Enter (optionally add passphrase)

```bash
# start ssh-agent
eval "$(ssh-agent -s)"

# add private key
ssh-add ~/.ssh/id_ed25519
```

---

## 🔑 Step 2: Add SSH Key to GitHub

```bash
cat ~/.ssh/id_ed25519.pub
```

* Copy the output
* Go to **GitHub → Settings → SSH and GPG keys → New SSH key**
* Paste and save

---

## 🪜 Step 3: Clone Repository (SSH)

```bash
git clone git@github.com:<username>/<repo>.git
cd <repo>
```

---

## 📂 Step 4: File Management

```bash
# create files
echo "# Git SSH Practice 🔐" > README.md
mkdir notes
echo "SSH Practice file" > notes/ssh.txt

# stage files
git add README.md notes/

# commit files
git commit -m "feat: add README and SSH notes"
```

---

### 🗑️ Delete or Rename

```bash
git rm unwanted.txt
git commit -m "remove unwanted file"

git mv oldname.txt newname.txt
git commit -m "rename oldname to newname"
```

---

## 📝 Step 5: .gitignore

```bash
cat > .gitignore <<EOF
*.log
*.pem
.env
EOF

git add .gitignore
git commit -m "chore: add .gitignore"
```

---

## 🚀 Step 6: Push Changes (No Password Needed 🚫🔑)

```bash
git push -u origin main
```

> ✅ With SSH, you won’t need to enter your username/password or token.

---

## 🔄 Step 7: Pull Changes

```bash
git pull origin main
```

---

## 🌿 Step 8: Branching

```bash
# create & switch branch
git checkout -b feature/ssh-demo

# add file
echo "SSH branch feature" > ssh-demo.txt
git add ssh-demo.txt
git commit -m "feat: add ssh demo file"

# push branch
git push -u origin feature/ssh-demo
```

---

## ⚡ Step 9: Merge Branch

```bash
git checkout main
git pull origin main
git merge feature/ssh-demo
git push origin main
```

---

## 🛠️ Step 10: Undo & Reset

```bash
git reset HEAD file.txt
git reset --soft HEAD~1
git reset --hard HEAD~1
git revert <commit-hash>
```

---

## 📦 Step 11: Tags

```bash
git tag v1.0.0-ssh
git push origin v1.0.0-ssh
```

---

## 🧰 Step 12: Useful Commands

```bash
git status
git log --oneline --graph
git diff
git branch -a
git remote -v
```

---

## ✅ Practice Checklist

* [ ] Generate SSH key & add to GitHub
* [ ] Clone repo using SSH
* [ ] Create, add, and commit files
* [ ] Delete & rename files
* [ ] Add `.gitignore`
* [ ] Push without password/token
* [ ] Pull updates from remote
* [ ] Create & merge branches
* [ ] Undo mistakes (reset/revert)
* [ ] Create tags & push them

---

## 🔒 Security Notes

* Protect your private key `(~/.ssh/id_ed25519)`
* Never share private keys, only add the public one to GitHub
* Use passphrases for extra protection
* Keep SSH agent running for seamless workflow.
