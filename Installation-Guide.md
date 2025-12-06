## 🚀 Step 1: Install Git

Ubuntu pe Git usually pre-installed hota hai, but let’s be sure.

```bash
sudo apt update
sudo apt install git -y
```

Check version:

```bash
git --version
```

Agar version aagaya → you're good. ✔️

---

## ⚙️ Step 2: Set Your Username & Email (VERY IMPORTANT for commits)

```bash
git config --global user.name "sahil shaikh"
git config --global user.email "your-email@example.com"
```

Check if applied:

```bash
git config --global --list
```

---

## 🔑 Step 3: Add SSH Key for GitHub (recommended, no password headache)

### Generate SSH Key:

```bash
ssh-keygen -t ed25519 -C "your-email@example.com"
```

Jab woh bole “Enter file to save key”, just press **Enter**.

Jab bole passphrase → optional but recommended.
(Ya phir Enter twice if you want no passphrase.)

### Start SSH Agent:

```bash
eval "$(ssh-agent -s)"
```

### Add your key:

```bash
ssh-add ~/.ssh/id_ed25519
```

---

## 📋 Step 4: Copy the SSH public key

```bash
cat ~/.ssh/id_ed25519.pub
```

Ye output copy → GitHub → Settings → SSH Keys → “New SSH Key” → paste.

---

## 🧪 Step 5: Test Connection

```bash
ssh -T git@github.com
```

Agar "Hi sahil! You've successfully authenticated…" type aaya → done 🔥

---

## 📦 Step 6: Clone / Push / Pull

### Clone repo:

```bash
git clone git@github.com:username/repo.git
```

### Add files:

```bash
git add .
```

### Commit:

```bash
git commit -m "first commit from ubuntu vm"
```

### Push:

```bash
git push origin main
```
