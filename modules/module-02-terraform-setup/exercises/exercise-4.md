
# 🧪 Exercise 5: Install and Use Git

## 🎯 Objective

Install Git, configure it with your name and email, clone the course repo, link it to GitHub, and commit your first change.

---

## 🧱 What You’ll Practice

- Installing Git
- Setting up your Git identity
- Cloning the repo
- Creating and switching branches
- Committing changes
- Linking a local repo with GitHub

---

## 🪜 Steps

### ✅ Step 1: Install Git

- **macOS**:
  ```bash
  brew install git
  ```

- **Ubuntu/Debian**:
  ```bash
  sudo apt update
  sudo apt install git
  ```

- **Windows**:  
  Download from: https://git-scm.com/download/win

---

### ✅ Step 2: Configure Git Identity

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

Use your real name and email (especially if using GitHub).

---

### ✅ Step 3: Initialize or Clone the Repository

To clone an existing repo:

```bash
git clone https://github.com/your-org/terraform-data-lake-upskill.git
cd terraform-data-lake-upskill
```

Or, if starting locally:

```bash
mkdir terraform-data-lake-upskill
cd terraform-data-lake-upskill
git init
```

---

### ✅ Step 4: Link to GitHub (if you created the repo locally)

1. Go to GitHub and **create a new repository**.
2. Then link your local project to it:

```bash
git remote add origin https://github.com/your-username/terraform-data-lake-upskill.git
git branch -M main
git push -u origin main
```

---

### ✅ Step 5: Create a Branch and Commit

```bash
git checkout -b feature/setup-script
touch hello.txt
echo "hello from terraform learners!" > hello.txt
git add hello.txt
git commit -m "Add hello.txt as a test file"
```

---

### ✅ Step 6: Push Your Branch

```bash
git push origin feature/setup-script
```

Then go to GitHub and open a **pull request** (PR) 🎉

---

## 🧠 Reflection

- Why is Git especially useful when collaborating on Terraform infrastructure?
- What kinds of changes would you want to review before merging?

---

## 🛡️ Optional: Set Up SSH Authentication with GitHub

> 📝 You can skip this section if HTTPS works fine for you.
> SSH is only required if you want a passwordless, secure, and persistent connection to GitHub.

### ✅ Step 1: Generate an SSH key (if you don’t have one)

```bash
ssh-keygen -t ed25519 -C "your.email@example.com"
```

Press **Enter** to accept the default path (`~/.ssh/id_ed25519`).

---

### ✅ Step 2: Start the SSH agent

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

---

### ✅ Step 3: Copy your public key

```bash
cat ~/.ssh/id_ed25519.pub
```

Copy the output.

---

### ✅ Step 4: Add SSH key to GitHub

1. Go to: https://github.com/settings/keys
2. Click **"New SSH key"**
3. Paste the public key
4. Click **Add SSH key**

---

### ✅ Step 5: Test the connection

```bash
ssh -T git@github.com
```

Expected result:

```bash
Hi your-username! You've successfully authenticated.
```

---

### ✅ Step 6: Change remote URL to SSH (optional)

```bash
git remote set-url origin git@github.com:your-username/terraform-data-lake-upskill.git
```

You can now push and pull over SSH securely!

---

➡️ **Next Exercise:** [🧪 Exercise 5: Final Verification](./exercise-5.md)