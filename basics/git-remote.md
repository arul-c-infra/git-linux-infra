# Git Remote

Git remote allows a local Git repository to communicate with a remote repository such as GitHub.

A remote repository is commonly used to:

* Store Git repositories centrally
* Share code and documentation
* Push local changes
* Pull changes from other team members
* Fetch remote changes
* Collaborate with other engineers

---

## 1. What is a Remote Repository?

A remote repository is a Git repository hosted on another system.

Examples:

* GitHub
* GitLab
* Bitbucket
* Internal Git servers

Example:

```text
Local Linux Server
       |
       | Git
       |
       v
GitHub Repository
```

For this project:

```text
Local Repository
       |
       | origin
       v
https://github.com/arul-c-infra/git-linux-infra
```

---

## 2. Check Existing Remotes

**Command:**

```bash
git remote
```

Example:

```text
origin
```

To see the remote URL:

```bash
git remote -v
```

**Example:**

```text
[root@gitbash branch]# git remote add origin https://github.com/arul-c-infra/git-linux-infra.git
[root@gitbash branch]#
[root@gitbash branch]# git remote
origin
[root@gitbash branch]# 
[root@gitbash branch]# git remote -v
origin  https://github.com/arul-c-infra/git-linux-infra.git (fetch)
origin  https://github.com/arul-c-infra/git-linux-infra.git (push)
[root@gitbash branch]# 
```

### Fetch vs Push

The remote normally has two URLs:

```text
fetch → Download changes from remote
push  → Upload changes to remote
```

---

## 3. What is `origin`?

`origin` is the default name Git normally gives to the remote repository when you clone a repository.

For example:

```bash
git clone https://github.com/arul-c-infra/git-linux-infra.git
```

Git automatically creates:

```text
origin
```

You can verify it:

```bash
git remote -v
```

Example:

```bash
[root@gitbash branch]# git clone https://github.com/arul-c-infra/git-linux-infra.git
Cloning into 'git-linux-infra'...
remote: Enumerating objects: 63, done.
remote: Counting objects: 100% (63/63), done.
remote: Compressing objects: 100% (58/58), done.
remote: Total 63 (delta 18), reused 0 (delta 0), pack-reused 0 (from 0)
Receiving objects: 100% (63/63), 31.49 KiB | 6.30 MiB/s, done.
Resolving deltas: 100% (18/18), done.
[root@gitbash branch]#
[root@gitbash branch]# ls -l
total 8
-rw-r--r--. 1 root root 45 Sep 23 12:00 dev.conf
drwxr-xr-x. 4 root root 49 Sep 23 12:38 git-linux-infra
-rw-r--r--. 1 root root 51 Sep 23 11:59 patching.md
[root@gitbash branch]# 
[root@gitbash branch]# cd git-linux-infra/
[root@gitbash git-linux-infra]# ls -l
total 4
-rw-r--r--. 1 root root 2519 Sep 23 12:38 README.md
drwxr-xr-x. 2 root root  148 Sep 23 12:38 basics
[root@gitbash git-linux-infra]# 
```

---

## 4. Add a Remote Repository

If you created a local repository using:

```bash
git init
```

you can connect it to GitHub using:

```bash
git remote add origin https://github.com/arul-c-infra/git-linux-infra.git
```

Verify:

```bash
git remote -v
```

Expected output:

```text
origin  https://github.com/arul-c-infra/git-linux-infra.git (fetch)
origin  https://github.com/arul-c-infra/git-linux-infra.git (push)
```

---

## 5. View Detailed Remote Information

Command:

```bash
git remote show origin
```

This displays information about the remote repository.

Example:

```text
* remote origin
  Fetch URL: https://github.com/arul-c-infra/git-linux-infra.git
  Push  URL: https://github.com/arul-c-infra/git-linux-infra.git
  HEAD branch: main
```

---

## 6. Rename a Remote

You can rename a remote using:

```bash
git remote rename origin upstream
```

Check:

```bash
git remote -v
```

Now the remote will be called:

```text
upstream
```

For most personal GitHub repositories, keeping the default name `origin` is recommended.

---

## 7. Change a Remote URL

If the remote URL changes:

```bash
git remote set-url origin https://github.com/arul-c-infra/git-linux-infra.git
```

Verify:

```bash
git remote -v
```

---

## 8. Remove a Remote

To remove a remote:

```bash
git remote remove origin
```

Verify:

```bash
git remote
```

No remote should be displayed.

> Removing a remote does not delete the GitHub repository. It only removes the remote connection from your local repository.

---

## 9. Git Remote with an Existing GitHub Repository

If the repository already exists on GitHub, the easiest method is:

```bash
git clone https://github.com/arul-c-infra/git-linux-infra.git
```

Then:

```bash
cd git-linux-infra
```

Check:

```bash
git remote -v
```

Expected:

```text
origin  https://github.com/arul-c-infra/git-linux-infra.git (fetch)
origin  https://github.com/arul-c-infra/git-linux-infra.git (push)
```

---

## 10. Local Repository to GitHub

If you start with a local project:

```bash
mkdir linux-project
cd linux-project
git init
```

Create a file:

```bash
echo "Linux Infrastructure Project" > README.md
```

Stage it:

```bash
git add README.md
```

Commit it:

```bash
git commit -m "Initial commit"
```

Connect the GitHub repository:

```bash
git remote add origin https://github.com/arul-c-infra/linux-project.git
```

Verify:

```bash
git remote -v
```

At this point, your local repository knows where the remote GitHub repository is located.

---

## 11. Remote Branches

To see remote branches:

```bash
git branch -r
```

Example:

```text
origin/main
origin/linux-patching
```

To see both local and remote branches:

```bash
git branch -a
```

Example:

```text
* main
  linux-patching
  remotes/origin/main
  remotes/origin/linux-patching
```

---

## 12. Remote Tracking

A local branch can track a remote branch.

Example:

```text
Local                         Remote

main  ---------------------> origin/main
       tracking relationship
```

You can see tracking information using:

```bash
git branch -vv
```

Example:

```text
* main abc1234 [origin/main] Update README
```

This means the local `main` branch is tracking `origin/main`.

---

## 13. Git Remote Workflow

A common workflow is:

```text
Local Repository
       |
       | git add
       ↓
Staging Area
       |
       | git commit
       ↓
Local Git Repository
       |
       | git push
       ↓
Remote Repository
       |
      GitHub
```

To get changes from GitHub:

```text
GitHub
  |
  | git fetch / git pull
  ↓
Local Repository
```

---

## 14. Practical Linux Infrastructure Example

Suppose you maintain Linux server documentation in GitHub.

You clone the repository:

```bash
git clone https://github.com/arul-c-infra/git-linux-infra.git
```

Enter the repository:

```bash
cd git-linux-infra
```

Check the remote:

```bash
git remote -v
```

Create a documentation branch:

```bash
git switch -c linux-monitoring
```

Make changes:

```bash
vim monitoring.md
```

Stage:

```bash
git add monitoring.md
```

Commit:

```bash
git commit -m "Add Linux monitoring documentation"
```

The commit currently exists only in your local repository.

Later, you can push the branch to GitHub:

```bash
git push -u origin linux-monitoring
```

This creates the remote branch:

```text
origin/linux-monitoring
```

---

## 15. Difference Between Local and Remote

| Location          | Example                            |
| ----------------- | ---------------------------------- |
| Working directory | Files you are currently editing    |
| Staging area      | Changes prepared for commit        |
| Local repository  | Commits stored on your system      |
| Remote repository | Repository hosted on GitHub/GitLab |

Example:

```text
Working Directory
       ↓
   git add
       ↓
Staging Area
       ↓
  git commit
       ↓
Local Repository
       ↓
   git push
       ↓
Remote Repository
```

---

## 16. Important Git Remote Commands

| Command              | Purpose                   |
| -------------------- | ------------------------- |
| `git remote`         | List remote names         |
| `git remote -v`      | Show remote URLs          |
| `git remote add`     | Add a remote              |
| `git remote show`    | Show remote details       |
| `git remote rename`  | Rename a remote           |
| `git remote set-url` | Change remote URL         |
| `git remote remove`  | Remove a remote           |
| `git branch -r`      | List remote branches      |
| `git branch -a`      | List all branches         |
| `git branch -vv`     | Show tracking information |

---

## 17. Key Takeaways

### Check remote

```bash
git remote -v
```

### Add remote

```bash
git remote add origin <repository-url>
```

### Change remote

```bash
git remote set-url origin <repository-url>
```

### View remote details

```bash
git remote show origin
```

### View remote branches

```bash
git branch -r
```

### Push a branch

```bash
git push -u origin <branch-name>
```

A remote connects your **local Git repository** with a **central repository such as GitHub**.

The most important concept is:

```text
Local Repository  ←→  Remote Repository
       Git               GitHub
```
