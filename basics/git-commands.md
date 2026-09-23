# Git Commands Reference

A practical reference for commonly used Git commands.

## 1. Git Configuration

### Check Git version

```bash
git --version
```

### Configure username

```bash
git config --global user.name "Arul C"
```

### Configure email

```bash
git config --global user.email "your-email@example.com"
```

### View Git configuration

```bash
git config --global --list
```

---

## 2. Repository Management

### Initialize a repository

```bash
git init
```

### Clone a repository

```bash
git clone <repository-url>
```

### Check repository status

```bash
git status
```

---

## 3. Tracking Changes

### Add a specific file

```bash
git add filename
```

### Add all changes

```bash
git add .
```

### Commit changes

```bash
git commit -m "Add Git documentation"
```

### View commit history

```bash
git log
```

### View compact commit history

```bash
git log --oneline
```

### View changes

```bash
git diff
```

---

## 4. Remote Repository

### View remote repositories

```bash
git remote -v
```

### Add a remote repository

```bash
git remote add origin <repository-url>
```

### Push changes

```bash
git push origin main
```

### Pull changes

```bash
git pull origin main
```

---

## 5. Branch Management

### List branches

```bash
git branch
```

### Create a branch

```bash
git branch feature-linux
```

### Switch to a branch

```bash
git switch feature-linux
```

### Create and switch to a new branch

```bash
git switch -c feature-linux
```

### Merge a branch

```bash
git merge feature-linux
```

### Delete a local branch

```bash
git branch -d feature-linux
```

---

## 6. Practical Infrastructure Workflow

Git can be used to manage infrastructure files such as:

* Linux shell scripts
* Ansible playbooks
* Dockerfiles
* Kubernetes YAML manifests
* Terraform configuration
* CloudFormation templates
* Infrastructure documentation

A typical workflow:

```text
Create Branch
     ↓
Make Changes
     ↓
git status
     ↓
git add .
     ↓
git commit
     ↓
git push
     ↓
Pull Request
     ↓
Code Review
     ↓
Merge
```

## 7. Useful Git Commands for Linux Administrators

```bash
git status
git branch
git switch
git add
git commit
git log
git diff
git clone
git pull
git push
git remote -v
```

These commands are useful for maintaining Linux administration scripts, infrastructure configuration, and automation code under version control.
