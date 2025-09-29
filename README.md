Acha 👍 samajh gaya bhai — tu chahta hai ek **master README** jo sirf **Git** ke topics ko cover kare:

* Git via HTTPS
* Git via SSH
* Git Branching

Aur wo bhi ekdum **attractive + detailed** style me.
Yeh le teri final **Git-focused README.md** 👇

---
# 🌀 Mastering Git – by Sahil Shaikh

Welcome to my **Git Practice Repository** 🎯  
This repo contains all my **hands-on Git exercises** – from basic file management to advanced branching strategies.  

---

## 🛠️ Topics Covered

### 🔑 Git with HTTPS Authentication
Learn to work with Git using **HTTPS** and Personal Access Tokens (PAT).  

**Steps Practiced:**
1. Initialize a repo → `git init`  
2. Connect remote (HTTPS) → `git remote add origin <url>`  
3. Add files → `git add <file>`  
4. Commit changes → `git commit -m "message"`  
5. Push to GitHub (with PAT) → `git push origin main`  
6. Pull updates → `git pull origin main`  
7. File management: create, delete, update, restore  

📌 [Detailed Guide](./git-https/README.md)

---

### 🔐 Git with SSH Authentication
Work with Git securely using **SSH keys** (no need to enter credentials every time).  

**Steps Practiced:**
1. Generate key → `ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`  
2. Add SSH key to agent → `ssh-add ~/.ssh/id_rsa`  
3. Copy public key → `cat ~/.ssh/id_rsa.pub`  
4. Add key to GitHub → *Settings → SSH Keys*  
5. Clone via SSH → `git clone git@github.com:user/repo.git`  
6. Push/Pull changes securely  

📌 [Detailed Guide](./git-ssh/README.md)

---

### 🌿 Git Branching & Merging
Practice working with **multiple branches** in Git.  

**Steps Practiced:**
1. Create new branch → `git branch feature-1`  
2. Switch branch → `git checkout feature-1`  
3. Add commits in branch → `git add . && git commit -m "feature work"`  
4. Push branch to GitHub → `git push origin feature-1`  
5. Merge into main →  
   - Switch → `git checkout main`  
   - Merge → `git merge feature-1`  
6. Resolve merge conflicts (if any)  
7. Delete branch → `git branch -d feature-1`  

📌 [Detailed Guide](./git-branches/README.md)

---

## 📂 Repository Structure

```bash
📦 git-practice-repo
├── git-https/              # Git via HTTPS practice
│   └── README.md
├── git-ssh/                # Git via SSH practice
│   └── README.md
├── git-branches/           # Branching & merging practice
│   └── README.md
└── README.md               # 👉 Main Git overview
````

---

## 📊 GitHub Stats

<p align="center">
  <img src="https://streak-stats.demolab.com?user=sahilshaikh867&theme=radical&border_radius=6" alt="GitHub Streak"/>
</p>

<p align="center">
  <img src="https://github-readme-stats.vercel.app/api?username=sahilshaikh867&show_icons=true&theme=radical" alt="GitHub Stats"/>
</p>

---

## 🌐 Connect with Me

[![LinkedIn](https://img.shields.io/badge/LinkedIn-blue?style=for-the-badge\&logo=linkedin\&logoColor=white)](https://www.linkedin.com/in/sahilshaikh867/)
[![Portfolio](https://img.shields.io/badge/Portfolio-grey?style=for-the-badge\&logo=vercel\&logoColor=white)](https://sahilshaikh867.vercel.app/)

---

## 🎯 Goal

This repo is my **Git playground** 🏗️
From HTTPS → SSH → Branching, I’m building the foundation for pro-level DevOps workflows 🚀.
