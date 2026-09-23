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

## 4. Add a Remote Repository:

**Create a repo in the server:**

```bash
[root@gitbash /]# mkdir linux-project
[root@gitbash /]# 
[root@gitbash /]# cd linux-project/
[root@gitbash linux-project]# 
[root@gitbash linux-project]# git init
Initialized empty Git repository in /linux-project/.git/
[root@gitbash linux-project]# 
[root@gitbash linux-project]# ls -l
total 0
[root@gitbash linux-project]# git config --global user.name "Arul C"
[root@gitbash linux-project]# 
[root@gitbash linux-project]# git config --global user.mail "salemarul1991@gmail.com"
[root@gitbash linux-project]# 
[root@gitbash linux-project]# echo "# Linux Project" > README.md
[root@gitbash linux-project]# 
[root@gitbash linux-project]# git add README.md
[root@gitbash linux-project]# 
[root@gitbash linux-project]# git commit -m "Initial commit"
[main (root-commit) 9463931] Initial commit
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
[root@gitbash linux-project]#
```

**Create an empty repository on GitHub:**

<img width="822" height="427" alt="image" src="https://github.com/user-attachments/assets/5d740d4a-367e-42c7-9aa4-44ab71968a82" />

**Connect your local repository to GitHub:**
```bash
[root@gitbash linux-project]# git remote add origin https://github.com/arul-c-infra/linux-project.git
[root@gitbash linux-project]# 
[root@gitbash linux-project]# git remote -v
origin  https://github.com/arul-c-infra/linux-project.git (fetch)
origin  https://github.com/arul-c-infra/linux-project.git (push)
[root@gitbash linux-project]#
```
**Generate the Token at GitHub:**
Profile --> Settings -->Developer Settings --> Personal Token Access -->Token Classic

**Push your local repository to GitHub:**
```bash
[root@gitbash linux-project]# git push -u origin main
Username for 'https://github.com': arul-c-infra
Password for 'https://arul-c-infra@github.com': -------> Use the above generated token
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 230 bytes | 230.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To https://github.com/arul-c-infra/linux-project.git
 * [new branch]      main -> main
branch 'main' set up to track 'origin/main'.
[root@gitbash linux-project]# 
```
**Verify the contents in the GitHub:**

<img width="1846" height="392" alt="image" src="https://github.com/user-attachments/assets/8fc9e2bd-40e5-4f0d-b5b5-a5263c790046" />

---

## 5. View Detailed Remote Information

**Command:**

```bash
git remote show origin
```

This displays information about the remote repository.

**Example:**

```text
[root@gitbash linux-project]# git remote show origin
* remote origin
  Fetch URL: https://github.com/arul-c-infra/linux-project.git
  Push  URL: https://github.com/arul-c-infra/linux-project.git
  HEAD branch: main
  Remote branch:
    main tracked
  Local branch configured for 'git pull':
    main merges with remote main
  Local ref configured for 'git push':
    main pushes to main (up to date)
[root@gitbash linux-project]# 
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

**Example:**

```text
[root@gitbash linux-project]# git remote rename origin upstream
Renaming remote references: 100% (1/1), done.
[root@gitbash linux-project]# 
[root@gitbash linux-project]# git remote -v
upstream        https://github.com/arul-c-infra/linux-project.git (fetch)
upstream        https://github.com/arul-c-infra/linux-project.git (push)
[root@gitbash linux-project]# 
```

For most personal GitHub repositories, keeping the default name `origin` is recommended.

---

## 7. Change a Remote URL

If the remote URL changes: unix_project

```bash
git remote set-url origin https://github.com/arul-c-infra/unix_project.git
```

Verify:
```bash
git remote -v
```
```bash
[root@gitbash linux-project]# git remote rename upstream origin
Renaming remote references: 100% (1/1), done.
[root@gitbash linux-project]# 
[root@gitbash linux-project]# git remote set-url origin https://github.com/arul-c-infra/unix_project.git
[root@gitbash linux-project]# 
[root@gitbash linux-project]# git remote -v
origin  https://github.com/arul-c-infra/unix_project.git (fetch)
origin  https://github.com/arul-c-infra/unix_project.git (push)
[root@gitbash linux-project]# 
[root@gitbash linux-project]# git push -u origin main
Username for 'https://github.com': arul-c-infra
Password for 'https://arul-c-infra@github.com': 
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 230 bytes | 230.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To https://github.com/arul-c-infra/unix_project.git
 * [new branch]      main -> main
branch 'main' set up to track 'origin/main'.
[root@gitbash linux-project]# 
[root@gitbash linux-project]# 
```
**Validate the same in the GitHub:**

<img width="1317" height="595" alt="image" src="https://github.com/user-attachments/assets/64e6c44d-2b3a-4e73-98f8-2ec12316cafe" />

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

```bash
[root@gitbash linux-project]# git remote remove origin
[root@gitbash linux-project]# 
[root@gitbash linux-project]# git remote -v
[root@gitbash linux-project]# 
```
> Removing a remote does not delete the GitHub repository. It only removes the remote connection from your local repository.

---

## 9. Git Remote with an Existing GitHub Repository

If the repository already exists on GitHub, the easiest method is:

```bash
git clone https://github.com/arul-c-infra/git-linux-infra.git
```

Then:

```bash
[root@gitbash /]# mkdir repo_clone
[root@gitbash /]# 
[root@gitbash /]# cd repo_clone/
[root@gitbash repo_clone]# 
[root@gitbash repo_clone]# 
[root@gitbash repo_clone]# git clone https://github.com/arul-c-infra/git-linux-infra.git
Cloning into 'git-linux-infra'...
remote: Enumerating objects: 67, done.
remote: Counting objects: 100% (67/67), done.
remote: Compressing objects: 100% (62/62), done.
remote: Total 67 (delta 20), reused 0 (delta 0), pack-reused 0 (from 0)
Receiving objects: 100% (67/67), 32.80 KiB | 861.00 KiB/s, done.
Resolving deltas: 100% (20/20), done.
[root@gitbash repo_clone]# 
[root@gitbash repo_clone]# ls -l
total 0
drwxr-xr-x. 4 root root 49 Sep 23 15:50 git-linux-infra
[root@gitbash repo_clone]# 
[root@gitbash repo_clone]# cd git-linux-infra/
[root@gitbash git-linux-infra]# 
[root@gitbash git-linux-infra]# ls -l
total 4
-rw-r--r--. 1 root root 2519 Sep 23 15:50 README.md
drwxr-xr-x. 2 root root  148 Sep 23 15:50 basics
[root@gitbash git-linux-infra]#

[root@gitbash git-linux-infra]# git remote -v
origin  https://github.com/arul-c-infra/git-linux-infra.git (fetch)
origin  https://github.com/arul-c-infra/git-linux-infra.git (push)
[root@gitbash git-linux-infra]# 
```

---
## 11. Remote Branches

To see remote branches:

```bash
git branch -r
```

Example:

```text
[root@gitbash git-linux-infra]# git branch -r
  origin/HEAD -> origin/main
  origin/main
[root@gitbash git-linux-infra]# 
```

To see both local and remote branches:

```bash
git branch -a
```

Example:

```text
[root@gitbash git-linux-infra]# git checkout -b feature-branch
Switched to a new branch 'feature-branch'
[root@gitbash git-linux-infra]# 
[root@gitbash git-linux-infra]# 
[root@gitbash git-linux-infra]# git switch main
Switched to branch 'main'
Your branch is up to date with 'origin/main'.
[root@gitbash git-linux-infra]#
[root@gitbash git-linux-infra]# git branch -a
  feature-branch
* main
  remotes/origin/HEAD -> origin/main
  remotes/origin/main
[root@gitbash git-linux-infra]# 
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
[root@gitbash git-linux-infra]# git branch -vv
  feature-branch 1368f97 Update git-remote.md
* main           1368f97 [origin/main] Update git-remote.md
[root@gitbash git-linux-infra]# 
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
