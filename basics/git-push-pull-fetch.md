# Git Push, Pull and Fetch

Git provides commands to synchronize changes between a local repository and a remote repository such as GitHub.

The three important commands are:

```text
git push
git pull
git fetch
```

---

## 1. Git Push

`git push` uploads local commits to a remote repository.

```text
Local Repository
       |
       | git push
       ↓
Remote Repository
```

### Basic Command

```bash
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

If the local branch is already connected to a remote branch, this is enough.
<img width="1317" height="595" alt="image" src="https://github.com/user-attachments/assets/28925458-ff10-4a92-96ed-9f0faf4c9902" />

---

## 2. Push a Specific Branch

Suppose you have:

```bash
git branch
```

Output:

```text
[root@gitbash linux-project]# git branch 
* feature-branch
  main
[root@gitbash linux-project]#
[root@gitbash linux-project]# git remote add origin https://github.com/arul-c-infra/linux-project.git
[root@gitbash linux-project]# 
[root@gitbash linux-project]# git remote -v
origin  https://github.com/arul-c-infra/linux-project.git (fetch)
origin  https://github.com/arul-c-infra/linux-project.git (push)
[root@gitbash linux-project]# 
[root@gitbash linux-project]# ls -l
total 8
-rw-r--r--. 1 root root 16 Sep 23 15:11 README.md
-rw-r--r--. 1 root root 15 Sep 23 16:36 linux_inventory
[root@gitbash linux-project]# 
[root@gitbash linux-project]# git push -u origin feature-branch
Username for 'https://github.com': arul-c-infra
Password for 'https://arul-c-infra@github.com': 
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 2 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 302 bytes | 302.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
remote: 
remote: Create a pull request for 'feature-branch' on GitHub by visiting:
remote:      https://github.com/arul-c-infra/linux-project/pull/new/feature-branch
remote: 
To https://github.com/arul-c-infra/linux-project.git
 * [new branch]      feature-branch -> feature-branch
branch 'feature-branch' set up to track 'origin/feature-branch'.
[root@gitbash linux-project]# 
```

---

## 3. Check Remote Branches

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
```bash
[root@gitbash linux-project]# git branch -r
  origin/feature-branch
[root@gitbash linux-project]# git branch -a
* feature-branch
  main
  remotes/origin/feature-branch
[root@gitbash linux-project]#
```

---

# 4. Git Fetch

`git fetch` downloads information about changes from the remote repository without changing your current working files.

```text
GitHub
   |
   | git fetch
   ↓
Local Repository
```

Command:
```bash
git fetch
```

Or:
```bash
git fetch origin
```

### Important

`git fetch` does **not** automatically merge the changes into your current branch.

It allows you to inspect the remote changes first.

Create a file in GitHub:
<img width="1327" height="545" alt="image" src="https://github.com/user-attachments/assets/cd032c0f-e5dc-4281-b875-7b8f8369aa1f" />


```bash
[root@gitbash linux-project]# git fetch origin
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (3/3), 926 bytes | 926.00 KiB/s, done.
From https://github.com/arul-c-infra/linux-project
   9463931..d78a279  main       -> origin/main
[root@gitbash linux-project]# 
```

---


## 5. Git Pull

`git pull` downloads changes from the remote repository and integrates them into your current branch.

Conceptually:

```text
git pull
    =
git fetch
    +
git merge
```

Command:

```bash
git pull
```

Or:

```diff
[root@gitbash linux-project]# git checkout main
Switched to branch 'main'
[root@gitbash linux-project]# 
[root@gitbash linux-project]#
[root@gitbash linux-project]# ls -l
total 8
-rw-r--r--. 1 root root 16 Sep 23 15:11 README.md
-rw-r--r--. 1 root root 15 Sep 23 16:53 linux_inventory
[root@gitbash linux-project]# 
[root@gitbash linux-project]# git merge feature-branch
Updating 9463931..45ba97c
Fast-forward
 linux_inventory | 8 ++++++++
 1 file changed, 8 insertions(+)
 create mode 100644 linux_inventory
[root@gitbash linux-project]#
[root@gitbash linux-project]# git pull origin main
From https://github.com/arul-c-infra/linux-project
 * branch            main       -> FETCH_HEAD
Updating 45ba97c..679e17c
Fast-forward
 newfile_pull | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 newfile_pull
[root@gitbash linux-project]# 
[root@gitbash linux-project]# ls -l
total 12
-rw-r--r--. 1 root root 16 Sep 23 15:11 README.md
-rw-r--r--. 1 root root 15 Sep 23 16:53 linux_inventory
-rw-r--r--. 1 root root  1 Sep 23 16:54 newfile_pull
[root@gitbash linux-project]# 
```

---

## 6. Push vs Pull vs Fetch

| Command     | Purpose                                 |
| ----------- | --------------------------------------- |
| `git push`  | Upload local commits to remote          |
| `git fetch` | Download remote changes without merging |
| `git pull`  | Download and integrate remote changes   |

Simple view:

```text
              GitHub
             /      \
            /        \
       push ↑          ↓ fetch
          /            \
         /              \
      Local Repository
             ↑
             |
            pull
```
---

# 7. Git Push Workflow

Suppose you modify a file:

```bash
vim README.md
```

Check:

```bash
git status
```

Stage the change:

```bash
git add README.md
```

Commit:

```bash
git commit -m "Update README"
```

Push:

```bash
git push
```

Complete workflow:

```text
Modify
  ↓
git add
  ↓
git commit
  ↓
git push
  ↓
GitHub
```

---

# 8. Git Fetch Workflow

When you want to check whether GitHub has new changes:

```bash
git fetch origin
```

Check branches:

```bash
git branch -a
```

Check recent commits:

```bash
git log --oneline --all
```

Compare your local branch with the remote:

```bash
git diff main..origin/main
```

This allows you to inspect remote changes before integrating them.

---

# 9. Git Pull Workflow

If you are ready to bring remote changes into your current branch:

```bash
git pull origin main
```

Typical workflow:

```text
GitHub
   ↓
git pull
   ↓
Local main
```

Before pulling important changes, it is good practice to check:

```bash
git status
```

Make sure you understand any local uncommitted changes first.

---

# 10. Local Changes and Git Pull

Suppose you modified a file locally:

```bash
vim monitoring.md
```

Check:

```bash
git status
```

If you have uncommitted changes, pulling may sometimes result in conflicts or Git may refuse to proceed.

A safe approach is to either commit the changes:

```bash
git add .
git commit -m "Update monitoring documentation"
```

or temporarily store them using:

```bash
git stash
```

`git stash` is covered separately in the Git stash guide.

---

# 11. Track a Remote Branch

After cloning a repository:

```bash
git clone <repository-url>
```

Git normally configures:

```text
local main
     ↕
origin/main
```

Check tracking:

```bash
git branch -vv
```

Example:

```text
* main abc1234 [origin/main] Update README
```

This means the local `main` branch tracks `origin/main`.

---

# 12. Push a New Branch

Create a branch:

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

Push:

```bash
git push -u origin linux-monitoring
```

Now the branch exists on GitHub.

---

# 13. Fetch a Specific Remote Branch

You can fetch a specific branch:

```bash
git fetch origin linux-monitoring
```

Then inspect it:

```bash
git log --oneline origin/linux-monitoring
```

---

# 14. Pull a Specific Branch

To pull changes from a specific remote branch:

```bash
git pull origin linux-monitoring
```

Normally, you should first switch to the local branch where you want those changes integrated.

---


# 15. Fetch vs Pull — Important Difference

### `git fetch`

```bash
git fetch origin
```

Downloads remote information but does not merge it into your current branch.

Use it when you want to **inspect changes first**.

### `git pull`

```bash
git pull origin main
```

Downloads remote changes and integrates them into your current branch.

Use it when you are ready to **bring remote changes into your local branch**.

### Simple rule

```text
Want to inspect first?
        ↓
    git fetch

Want to download + integrate?
        ↓
    git pull
```

---

# 16. Common Commands

### Push current branch

```bash
git push
```

### First push

```bash
git push -u origin main
```

### Push a feature branch

```bash
git push -u origin feature-name
```

### Fetch all remote changes

```bash
git fetch origin
```

### Fetch all remotes

```bash
git fetch --all
```

### Pull current branch

```bash
git pull
```

### Pull from a specific branch

```bash
git pull origin main
```

### View remote branches

```bash
git branch -r
```

### View all branches

```bash
git branch -a
```

---

# 17. Common Errors

## Error: No upstream branch

You may see:

```text
fatal: The current branch main has no upstream branch.
```

Set the upstream:

```bash
git push -u origin main
```

After that:

```bash
git push
```

will normally work.

---

## Error: Non-fast-forward

You may see:

```text
! [rejected] main -> main (non-fast-forward)
```

This usually means the remote branch contains commits that your local branch does not have.

First inspect the remote:

```bash
git fetch origin
```

Then check:

```bash
git log --oneline --all
```

Do not immediately overwrite the remote branch with force push. Understand the branch history first.

---

# 18. Recommended Workflow

For a normal daily Git workflow:

```bash
git status
git pull
```

Make your changes:

```bash
vim file.md
```

Check:

```bash
git status
git diff
```

Stage:

```bash
git add .
```

Review staged changes:

```bash
git diff --staged
```

Commit:

```bash
git commit -m "Update Linux documentation"
```

Push:

```bash
git push
```

Complete workflow:

```text
          GitHub
            ↑
            | git push
            |
      Local Repository
            ↑
         git commit
            ↑
          git add
            ↑
      Working Directory

          GitHub
            |
            | git fetch / git pull
            ↓
      Local Repository
```

---

# 19. Summary

| Command     | Direction      | Integration                       |
| ----------- | -------------- | --------------------------------- |
| `git push`  | Local → Remote | Uploads commits                   |
| `git fetch` | Remote → Local | Downloads remote information only |
| `git pull`  | Remote → Local | Downloads and integrates changes  |

### Remember

```bash
# Upload
git push

# Download remote information
git fetch

# Download and integrate
git pull
```

The key concept is:

```text
git push
Local ───────────────→ GitHub


git fetch
Local ←─────────────── GitHub
       (inspect first)


git pull
Local ←─────────────── GitHub
       (download + integrate)
```

For Linux infrastructure teams, understanding the difference between `fetch` and `pull` is especially useful because `fetch` allows you to inspect remote changes before integrating them into your working branch.
