# Git init
# Git Init, Add and Commit

This guide explains the basic Git workflow using `git init`, `git add`, and `git commit`.

---

## 1. Git Init

`git init` initializes a new Git repository in the current directory.

### Command

```bash
git init
```

### Example

```bash
mkdir linux-project
cd linux-project
git init
```

### Expected Output

```text
Initialized empty Git repository in /home/ec2-user/linux-project/.git/
```

The `.git` directory contains the Git repository metadata.

### Verify

```bash
ls -la
```

You should see:

```text
.git
```

### Check Repository Status

```bash
git status
```

Example:

```text
On branch main

No commits yet

nothing to commit
```

> **Note:** Use `git init` when starting a new local Git repository. If a repository already exists on GitHub, normally use `git clone` instead.

---

## 2. Git Add

`git add` moves changes from the **working directory** to the **staging area**.

### Create a File

```bash
echo "Linux Infrastructure" > server.txt
```

Check the status:

```bash
git status
```

Example:

```text
Untracked files:
  server.txt
```

### Add a Specific File

```bash
git add server.txt
```

Check again:

```bash
git status
```

Example:

```text
Changes to be committed:
  new file: server.txt
```

### Add Multiple Files

```bash
git add file1.txt file2.txt
```

### Add All Changes

```bash
git add .
```

> `git add .` stages new files, modified files, and deleted files under the current directory.

---

## 3. Git Commit

`git commit` saves the staged changes into the local Git repository.

### Command

```bash
git commit -m "Add server documentation"
```

Example output:

```text
[main abc1234] Add server documentation
 1 file changed, 1 insertion(+)
 create mode 100644 server.txt
```

### Verify the Commit

```bash
git log --oneline
```

Example:

```text
abc1234 Add server documentation
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

## 5. Example: Complete Workflow

Create a new project:

```bash
mkdir linux-project
cd linux-project
```

Initialize Git:

```bash
git init
```

Create a file:

```bash
echo "Linux Server Administration" > README.md
```

Check status:

```bash
git status
```

Stage the file:

```bash
git add README.md
```

Check staged changes:

```bash
git status
```

Commit the change:

```bash
git commit -m "Add Linux administration README"
```

View commit history:

```bash
git log --oneline
```

---

## 6. Git Status

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

## 7. Git Add vs Git Commit

| Command      | Purpose                                 |
| ------------ | --------------------------------------- |
| `git init`   | Create a new local Git repository       |
| `git add`    | Move changes to staging area            |
| `git commit` | Save staged changes to local repository |
| `git status` | Check current Git state                 |
| `git log`    | View commit history                     |

---

## 8. Important Difference

### `git add`

```bash
git add server.conf
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

## 9. Git Init vs Git Clone

### New local project

Use:

```bash
git init
```

Example:

```bash
mkdir my-project
cd my-project
git init
```

### Existing GitHub repository

Use:

```bash
git clone https://github.com/arul-c-infra/git-linux-infra.git
```

Then:

```bash
cd git-linux-infra
```

**Do not normally run `git init` inside a repository that you have already cloned.**

---

## 10. Linux Infrastructure Example

Suppose a Linux administrator creates a configuration documentation file:

```bash
echo "NTP configuration" > ntp-config.md
```

Check:

```bash
git status
```

Stage:

```bash
git add ntp-config.md
```

Review:

```bash
git diff --staged
```

Commit:

```bash
git commit -m "Add NTP configuration documentation"
```

Verify:

```bash
git log --oneline
```

This provides a basic audit trail of infrastructure documentation changes.

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
