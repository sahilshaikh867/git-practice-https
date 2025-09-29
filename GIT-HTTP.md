# 🚀 Full Git (HTTPS) Cheat Sheet — Start → Finish (with examples)

> Assumption: tu Git Bash / terminal use kar raha hai (Windows, macOS, Linux). Replace `<username>`, `<repo>`, `<instance>`, `<email>` etc. apne values se.

---

## 0) Quick setup — install & global config

```bash
# check git
git --version

# set identity (do this once)
git config --global user.name "Sahil Shaikh"
git config --global user.email "your_email@example.com"

# helpful defaults (optional)
git config --global core.editor "code --wait"   # VSCode as editor
git config --global pull.rebase false           # default merge on pull (or true for rebase)
```

---

## 1) Create repo on GitHub (HTTPS flow)

1. GitHub → New → Repository

   * Name: `git-practice-https`
   * Public (or private)
   * **Do not** init with README (we'll do that locally)
2. Copy HTTPS URL: `https://github.com/<username>/git-practice-https.git`

---

## 2) Clone repo (HTTPS)

```bash
git clone https://github.com/<username>/git-practice-https.git
cd git-practice-https
```

---

## 3) Local file management (create / add / delete / rename / move)

### Create files / folders

```bash
# create README
echo "# My First HTTPS Git Repo 🚀" > README.md

# create folder + file
mkdir docs
echo "Some notes" > docs/notes.txt
```

### See status

```bash
git status
```

### Stage files (add)

```bash
git add README.md            # add a single file
git add docs/                 # add a folder (all files inside)
git add .                     # add everything (be careful)
git add -p                    # interactively stage hunks (awesome for precise commits)
```

### Commit staged changes

```bash
git commit -m "feat: add README and notes"
# or open editor
git commit
```

### Remove/delete files

```bash
git rm file.txt               # remove and stage deletion
git rm --cached secret.txt    # stop tracking file but keep it locally (useful for .gitignore corrections)
# If you used rm first:
rm oldfile.txt
git add -A                    # stage deletion for next commit
git commit -m "remove oldfile"
```

### Rename / Move

```bash
git mv oldname.txt newname.txt
git mv app/module1 app/module2
git commit -m "rename/move files"
```

### Update file (edit -> stage -> commit)

```bash
# edit file in editor, then
git add modified-file.txt
git commit -m "fix: update README content"
```

---

## 4) .gitignore (ignore files)

```bash
# create .gitignore
cat > .gitignore <<EOF
# OS
.DS_Store
Thumbs.db

# Editors
.vscode/
*.log

# Secrets
*.pem
*.key
.env

# Node / Python / etc
node_modules/
__pycache__/
EOF

git add .gitignore
git commit -m "chore: add .gitignore"
```

> If you already tracked a file that should be ignored: `git rm --cached path/to/file && git commit -m "stop tracking file"`

---

## 5) First push (HTTPS) — auth with Personal Access Token (PAT)

### Option A — Use Git prompt (recommended)

When you run:

```bash
git push -u origin main
```

Git will prompt for username → enter GitHub username.
Password → paste **Personal Access Token (PAT)** (NOT your GitHub password).

### How to create PAT (on GitHub):

* Go to GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic) OR Fine-grained tokens
* Create new token:

  * Scopes: check `repo` (for full repo access) or fine-grained repo access as needed.
  * Expiry: choose reasonable expiry.
* Copy the token **immediately** (you won’t see it again).

**Security note:** Do NOT paste token into commands visible to shell history or scripts. Use credential helper instead.

### Option B — Configure credential helper (so you don’t paste every time)

* Cache for a time (Linux/macOS):

```bash
git config --global credential.helper 'cache --timeout=3600'  # cache for 1 hour
```

* Store permanently (plaintext — **only on private machine**):

```bash
git config --global credential.helper store
# next push, Git will ask for credentials and then store them at ~/.git-credentials (plaintext)
```

* Windows (secure): Git for Windows ships with Git Credential Manager (GCM) which stores creds securely:

```bash
git config --global credential.helper manager-core
```

> Once credential helper is configured, `git push` will save PAT securely (or cache) and future pushes won't ask.

---

## 6) Typical workflow — commit & push

```bash
# check changes
git status

# stage changes
git add .

# commit
git commit -m "feat: add awesome feature"

# push to origin main
git push origin main
```

---

## 7) Pulling & staying in sync

```bash
# pull remote changes (will merge by default)
git pull origin main

# or pull with rebase
git pull --rebase origin main
```

If push is rejected (non-fast-forward), do:

```bash
git pull --rebase origin main
# resolve conflicts if any, then
git push origin main
```

---

## 8) Branching & feature flow (very important)

```bash
# create & switch
git checkout -b feature/xyz

# work -> add -> commit
git add .
git commit -m "feat: start feature xyz"

# push branch to remote
git push -u origin feature/xyz
```

Now open GitHub and create a Pull Request (PR) from `feature/xyz` to `main`. After review, merge on GitHub or via CLI.

Merge locally:

```bash
git checkout main
git pull origin main
git merge feature/xyz              # or git rebase feature/xyz (careful)
git push origin main
```

Delete branch after merge:

```bash
git branch -d feature/xyz            # delete local
git push origin --delete feature/xyz # delete remote
```

---

## 9) Resolve conflicts (practical)

If `git pull` or `git merge` leads to conflicts:

1. Git will mark conflicted files. Run `git status`.
2. Open files, look for `<<<<<<`, `======`, `>>>>>>>` markers. Edit to resolve.
3. Stage resolved files: `git add resolved-file`
4. Complete merge: `git commit` (if required) then `git push`.

Tip: `git mergetool` can help if configured.

---

## 10) Undo mistakes — safe to dangerous

### Unstage (keep changes)

```bash
git reset HEAD file.txt    # unstage file
```

### Revert last commit but keep changes staged

```bash
git reset --soft HEAD~1
```

### Revert last commit and unstaged changes

```bash
git reset --mixed HEAD~1   # default
```

### Discard all local changes (DANGEROUS)

```bash
git reset --hard HEAD
git clean -fd              # remove untracked files & dirs (use with caution)
```

### Revert a pushed commit (safe history)

```bash
git revert <commit-hash>   # creates a new commit that undoes the change
git push origin main
```

### Force push (use only if you know consequences)

```bash
git push --force-with-lease origin branch-name
```

`--force-with-lease` is safer than `--force`.

---

## 11) Stash (temporary save)

```bash
git stash save "WIP: debugging"
git stash list
git stash pop         # apply and remove from stash
git stash apply stash@{1} # apply specific stash
```

---

## 12) Tags & Releases

```bash
# create lightweight tag
git tag v1.0.0

# annotated tag
git tag -a v1.0.0 -m "Release v1.0.0"

# push tag
git push origin v1.0.0

# push all tags
git push origin --tags
```

---

## 13) Handling large files (Git LFS)

If files > 100 MB or many binaries:

```bash
# install LFS and track
git lfs install
git lfs track "*.zip"
git add .gitattributes
git add bigfile.zip
git commit -m "Add large binary via LFS"
git push origin main
```

---

## 14) Useful git commands cheat-sheet

```text
git status                # see current state
git log --oneline --graph # history
git show <commit>
git diff                  # unstaged changes
git diff --staged         # staged changes
git branch -a             # list branches (local & remote)
git remote -v             # remote URLs
git fetch origin          # update remote refs without merging
git pull origin main
git push origin <branch>
```

---

## 15) Authentication pitfalls & tips (HTTPS)

* GitHub passwords are **not supported** for git ops — use PAT.
* **Do not** put PAT in a committed file or in remote URL that will be stored in shell history.
* Prefer credential helpers (manager-core or store/cache).
* To remove saved credentials:

  * `git credential-reject` (rare), or delete `~/.git-credentials` if store used.
  * On Windows, use Windows Credential Manager UI.
* To revoke a PAT: GitHub → Settings → Developer settings → Personal access tokens → Revoke.

**Unsafe example (don’t do in public):**

```bash
# Avoid embedding token in URL (exposes token in history)
git remote set-url origin https://<username>:<PAT>@github.com/<username>/<repo>.git
```

---

## 16) Complete end-to-end example (one-shot — follow in sequence)

```bash
# 0 - clone the repo (created on GitHub)
git clone https://github.com/<username>/git-practice-https.git
cd git-practice-https

# 1 - create files
echo "# Git practice" > README.md
mkdir src
echo "console.log('hi')" > src/app.js

# 2 - stage & commit
git add .
git commit -m "chore: init repo with README and src"

# 3 - push (first push asks for username + PAT)
git push -u origin main

# 4 - create branch, add file
git checkout -b feature/login
echo "login code" > src/login.js
git add src/login.js
git commit -m "feat: add login module"
git push -u origin feature/login

# 5 - make change on main (simulate remote change)
# (on GitHub or another clone) -> commit & push to main

# 6 - update local main
git checkout main
git pull origin main

# 7 - merge branch
git merge feature/login
git push origin main
```

---

## 17) Advanced: interactive rebase (cleanup commits)

```bash
git checkout feature/xyz
git rebase -i HEAD~3  # edit last 3 commits interactively (squash/fixup/reorder)
# after rebase, force push
git push --force-with-lease origin feature/xyz
```

Use this for cleaning commits **before** merging to main.

---

## 18) Common errors & fixes

* `error: failed to push some refs` → someone pushed changes first. Do `git pull --rebase origin main`, resolve conflicts, then `git push`.
* `remote: Permission to ... denied` → likely auth issue (wrong creds or no access). Check PAT scopes and username.
* `fatal: unable to access 'https://...': Could not resolve host` → network/DNS issue.
* Merge conflicts → edit files to resolve conflict markers then `git add` + `git commit`.

---

## 19) Practical assignment (do this now — step-by-step)

1. Create GitHub repo `git-practice-https`.
2. Clone via HTTPS.
3. Follow the **Complete example** in section 16.
4. Create branch `feature/demo`, add a file, push the branch.
5. On GitHub, open a PR and merge.
6. Test `git pull` on your local to get merged changes.
7. Create a PAT with `repo` scope and push again if prompted.
8. Practice `git revert <commit>` and `git reset --soft HEAD~1`.

---

## 20) Safety & best practices (short)

* Write good commit messages: `type(scope): short summary` (Conventional Commits style).
* Don’t commit secrets; use `.gitignore` or secret managers.
* Use branches for features; keep `main` stable.
* Prefer `--force-with-lease` over `--force`.
* Revoke unused PATs.

---

## TL;DR — Minimal commands to remember

```bash
git clone https://github.com/<u>/<repo>.git
git status
git add .
git commit -m "msg"
git push origin main
git checkout -b feature/x
git push -u origin feature/x
git pull origin main
```

