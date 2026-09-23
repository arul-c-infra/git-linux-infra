# Git Init, Add and Commit

This guide explains the basic Git workflow using `git init`, `git add`, and `git commit`.
---

## 1. Git Init

`git init` initializes a new Git repository in the current directory.

### Command

```bash
git init
```
**Example:**
```bash
[root@gitbash /]# mkdir demogit
[root@gitbash /]# 
[root@gitbash /]# cd demogit/
[root@gitbash demogit]# 
[root@gitbash demogit]# git init
Initialized empty Git repository in /demogit/.git/
[root@gitbash demogit]# 
[root@gitbash demogit]# ls -l
total 0
[root@gitbash demogit]# ls -la
total 0
drwxr-xr-x.  3 root root  18 Sep 23 09:27 .
dr-xr-xr-x. 19 root root 252 Sep 23 09:27 ..
drwxr-xr-x.  6 root root 103 Sep 23 09:27 .git
[root@gitbash demogit]#
```
The `.git` directory contains the Git repository metadata.

### Check Repository Status

```bash
git status
```
**Output:**
```bash
[root@gitbash demogit]# git status
On branch main

No commits yet

nothing to commit (create/copy files and use "git add" to track)
[root@gitbash demogit]# 
```

> **Note:** Use `git init` when starting a new local Git repository. If a repository already exists on GitHub, normally use `git clone` instead.

---

## 2. Git Add

`git add` moves changes from the **working directory** to the **staging area**.

### Create a File

```bash
echo "Linux Infrastructure" > server.txt
```
**Output:**

```bash
[root@gitbash demogit]# echo "Linux Infrastructure" > server.txt
[root@gitbash demogit]# 
[root@gitbash demogit]# git status
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        server.txt

nothing added to commit but untracked files present (use "git add" to track)
[root@gitbash demogit]# 
```

### Add a Specific File

```bash
git add server.txt
```

Check again:

```bash
[root@gitbash demogit]# git add server.txt 
[root@gitbash demogit]# 
[root@gitbash demogit]# git status
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   server.txt

[root@gitbash demogit]# 
```

### Add Multiple Files

```bash
[root@gitbash demogit]# git add java.txt network.txt 
[root@gitbash demogit]# 
```


### Add All Changes

```bash
git add .
```

> `git add .` stages new files, modified files, and deleted files under the current directory.

```bash
[root@gitbash demogit]# git status
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   java.txt
        new file:   network.txt
        new file:   server.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        ref.txt
        test.txt

[root@gitbash demogit]# 
[root@gitbash demogit]# git add .
[root@gitbash demogit]# 
[root@gitbash demogit]# git status
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   java.txt
        new file:   network.txt
        new file:   ref.txt
        new file:   server.txt
        new file:   test.txt

[root@gitbash demogit]#
```

---

## 3. Git Commit

`git commit` saves the staged changes into the local Git repository.

### Command

```bash
git commit -m "Add server documentation"
```

Example output:

```bash
[root@gitbash demogit]# rm -f java.txt network.txt ref.txt test.txt 
[root@gitbash demogit]# 
[root@gitbash demogit]# ls -l
total 4
-rw-r--r--. 1 root root 21 Sep 23 09:36 server.txt
[root@gitbash demogit]# 
[root@gitbash demogit]# git commit -m "Add server documentation"
[main (root-commit) 4b393e0] Add server documentation
 5 files changed, 1 insertion(+)
 create mode 100644 java.txt
 create mode 100644 network.txt
 create mode 100644 ref.txt
 create mode 100644 server.txt
 create mode 100644 test.txt
[root@gitbash demogit]# 
[root@gitbash demogit]# git log
commit 4b393e09cdf9a4955ba7640f4ea297fa04d49d97 (HEAD -> main)
Author: Arul C <salemarul1991@gmail.com>
Date:   Wed Sep 23 09:45:09 2026 +0000

    Add server documentation
[root@gitbash demogit]# 
```

### Verify the Commit

```bash
git log --oneline
```

Example:

```text
[root@gitbash demogit]# git log --oneline
4b393e0 (HEAD -> main) Add server documentation
[root@gitbash demogit]# 
```

---

## 4. Basic Git Workflow

The basic workflow is:

```text
Working Directory
       |
       | git add
       v
Staging Area
       |
       | git commit
       v
Local Repository
```

### Commands

```bash
git status
git add .
git status
git commit -m "Add documentation"
git log --oneline
```
---

## 5. Git Status

`git status` is one of the most important Git commands.

```bash
git status
```

It shows:

* Current branch
* Untracked files
* Modified files
* Staged files
* Changes ready for commit

For Linux infrastructure work, use `git status` frequently before committing changes.

---

## 6. Git Add vs Git Commit

| Command      | Purpose                                 |
| ------------ | --------------------------------------- |
| `git init`   | Create a new local Git repository       |
| `git add`    | Move changes to staging area            |
| `git commit` | Save staged changes to local repository |
| `git status` | Check current Git state                 |
| `git log`    | View commit history                     |

---

## 7. Important Difference

### `git add`

```bash
git add server.txt
```

Means:

> "I want this change to be included in my next commit."

### `git commit`

```bash
git commit -m "Update server configuration"
```

Means:

> "Save the staged changes as a Git commit."

---

## 8. Git Init vs Git Clone

### New local project

Use:

```bash
git init
```

Example:

```bash
[root@gitbash /]# mkdir demogit
[root@gitbash /]# 
[root@gitbash /]# cd demogit/
[root@gitbash demogit]# 
[root@gitbash demogit]# git init
Initialized empty Git repository in /demogit/.git/
[root@gitbash demogit]# 
```

### Existing GitHub repository

Use:

```bash
git clone https://github.com/arul-c-infra/gitpractice
```

Then:

```bash
cd gitpractice
```
**Output:**

```bash
[root@gitbash ~]# pwd
/root
[root@gitbash ~]# git clone https://github.com/arul-c-infra/gitpractice
Cloning into 'gitpractice'...
remote: Enumerating objects: 6, done.
remote: Counting objects: 100% (6/6), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 6 (delta 0), reused 6 (delta 0), pack-reused 0 (from 0)
Receiving objects: 100% (6/6), done.
[root@gitbash ~]# 
[root@gitbash ~]# ls -l
total 0
drwxr-xr-x. 3 root root 30 Sep 23 09:52 gitpractice
[root@gitbash ~]# 
[root@gitbash ~]# cd gitpractice/
[root@gitbash gitpractice]# 
[root@gitbash gitpractice]# ls -l
total 4
-rw-r--r--. 1 root root 43 Sep 23 09:52 java
[root@gitbash gitpractice]# 
```

**Do not normally run `git init` inside a repository that you have already cloned.**
---

## Key Takeaways

```text
git init
    ↓
Create Git repository

git add
    ↓
Stage changes

git commit
    ↓
Save changes to local repository
```

### Remember

```bash
git init
git status
git add .
git status
git commit -m "Meaningful commit message"
git log --oneline
```

The complete workflow is:

**Working Directory → Staging Area → Local Repository**

