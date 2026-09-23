# Git Log and Diff

This guide covers Git commands used to review commit history, inspect commits, and identify changes between files, commits, and branches.

These commands are useful for Linux administrators and infrastructure engineers when reviewing changes to scripts, configuration files, Dockerfiles, Kubernetes manifests, Ansible playbooks, and infrastructure code.

---

## 1. `git log`

Displays the commit history of the current repository.

### Command

```bash
git log
```

### Example Output

```text
[root@gitbash demogit]# git log
commit 5bb8e2efd06872c54dd60a830ae2ada489a5116a (HEAD -> main)
Author: Arul C <salemarul1991@gmail.com>
Date:   Wed Sep 23 10:00:24 2026 +0000

    NTP conf added

commit 4b393e09cdf9a4955ba7640f4ea297fa04d49d97
Author: Arul C <salemarul1991@gmail.com>
Date:   Wed Sep 23 09:45:09 2026 +0000

    Add server documentation
[root@gitbash demogit]# 
```

> The commit ID, author, and date will be different depending on your repository.

### Use Case

Useful for checking the history of changes made to a repository.

---

## 2. `git log --oneline`

Displays commit history in a compact format.

### Command

```bash
git log --oneline
```

### Example Output

```text
[root@gitbash demogit]# git log --oneline
5bb8e2e (HEAD -> main) NTP conf added
4b393e0 Add server documentation
[root@gitbash demogit]# 
```

### Use Case

Useful when you want to quickly review recent commits.

---

## 3. `git log --oneline --graph`

Displays commits in a simple graphical structure.

### Command

```bash
git log --oneline --graph --all
```

### Example Output

```text
[root@gitbash demogit]# git log --oneline --graph
* 5bb8e2e (HEAD -> main) NTP conf added
* 4b393e0 Add server documentation
[root@gitbash demogit]# 
[root@gitbash demogit]# git log --oneline --graph --all
* 5bb8e2e (HEAD -> main) NTP conf added
* 4b393e0 Add server documentation
[root@gitbash demogit]# 
```
---

## 4. `git show`

Displays information about a specific commit.

### Command

```bash
git show <commit-id>
```


### Example Output

```text
[root@gitbash demogit]# git show 5bb8e2e
commit 5bb8e2efd06872c54dd60a830ae2ada489a5116a (HEAD -> main)
Author: Arul C <salemarul1991@gmail.com>
Date:   Wed Sep 23 10:00:24 2026 +0000

    NTP conf added

diff --git a/ntp.conf b/ntp.conf
new file mode 100644
index 0000000..e626b9f
--- /dev/null
+++ b/ntp.conf
@@ -0,0 +1 @@
+NTP configuration
[root@gitbash demogit]# 
```

### Use Case

Useful when you need to investigate exactly what was changed in a particular commit.

---

# Git Diff

## 5. `git diff`

Displays changes that have been made but are not yet staged.

### Example

Suppose a file contains:

```text
Linux Infrastructure
```

You change it to:

```text
Linux Cloud Infrastructure server
```

Run:

```bash
git diff
```

### Example Output

```diff
diff --git a/server.txt b/server.txt
index ab7bff0..8020a5a 100644
--- a/server.txt
+++ b/server.txt
@@ -1 +1 @@
-Linux Infrastructure
+Linux Cloud Infrastructure server
```

The `-` represents the old content.

The `+` represents the new content.

### Use Case

Review changes before adding them to the staging area.

---

## 6. `git diff --staged`

Displays changes that have already been added to the staging area.

### Commands

```bash
git add server.txt
```

Then:

```bash
git diff --staged
```

### Example Output

```diff
[root@gitbash demogit]# git diff --staged
diff --git a/server.txt b/server.txt
index ab7bff0..c5cf900 100644
--- a/server.txt
+++ b/server.txt
@@ -1 +1 @@
-Linux Infrastructure
+Linux Cloud Infrastructure server - RHEL
[root@gitbash demogit]# 
```

### Use Case

Useful for reviewing exactly what will be included in the next commit.

---

## 7. `git diff HEAD`

Shows the difference between the current working directory/staging state and the latest commit.

### Command

```bash
git diff HEAD
```

```diff
git diff HEAD
diff --git a/ntp.conf b/ntp.conf
index e626b9f..c890cfa 100644
--- a/ntp.conf
+++ b/ntp.conf
@@ -1 +1 @@
-NTP configuration
+NTP configuration setup
diff --git a/ref.txt b/ref.txt
deleted file mode 100644
index e69de29..0000000
diff --git a/server.txt b/server.txt
index ab7bff0..c5cf900 100644
--- a/server.txt
+++ b/server.txt
@@ -1 +1 @@
-Linux Infrastructure
+Linux Cloud Infrastructure server - RHEL
diff --git a/test.txt b/test.txt
deleted file mode 100644
index e69de29..0000000
```

### Use Case

Useful for reviewing all current changes against the latest committed version.

---

## 8. Compare Two Commits

You can compare two commits using:

```bash
git diff <commit1> <commit2>
```

### Example

```diff
[root@gitbash demogit]# git diff 5b8b60b ea14fff
diff --git a/50-redhat.conf b/50-redhat.conf
index 354c4c9..66c7d4b 100644
--- a/50-redhat.conf
+++ b/50-redhat.conf
@@ -19,4 +19,4 @@ X11Forwarding yes
 # It is recommended to use pam_motd in /etc/pam.d/sshd instead of PrintMotd,
 # as it is more configurable and versatile than the built-in version.
 PrintMotd no
-PermitRootLogin no
+PermitRootLogin yes
[root@gitbash demogit]# 
```

This shows the differences between the two commits.

### Use Case

Useful when investigating what changed between two versions of infrastructure code.

---

## 9. Compare Two Branches

You can compare two branches:

```bash
git diff main feature-linux
```

### Example

```text
main
   │
   └── Current production version

feature-linux
   │
   └── Proposed changes
```

### Use Case

Useful for reviewing changes before merging a feature branch into `main`.

```diff
[root@gitbash demogit]# git branch
* main
[root@gitbash demogit]# 
[root@gitbash demogit]# git checkout -b feature-linux
Switched to a new branch 'feature-linux'
[root@gitbash demogit]# 
[root@gitbash demogit]# ls -l
total 12
-rw-r--r--. 1 root root 737 Sep 23 10:19 50-redhat.conf
-rw-r--r--. 1 root root  24 Sep 23 10:10 ntp.conf
-rw-r--r--. 1 root root  41 Sep 23 10:08 server.txt
[root@gitbash demogit]# 
[root@gitbash demogit]# git branch
* feature-linux
  main
[root@gitbash demogit]# vi ntp.conf    
[root@gitbash demogit]# git add ntp.conf 
[root@gitbash demogit]# 
[root@gitbash demogit]# git diff main feature-linux
[root@gitbash demogit]# 
[root@gitbash demogit]# git commit -m "NTP at feature branch"
[feature-linux 1498157] NTP at feature branch
 1 file changed, 1 insertion(+), 1 deletion(-)
[root@gitbash demogit]# 
[root@gitbash demogit]# git diff main feature-linux
diff --git a/ntp.conf b/ntp.conf
index e626b9f..d1692ab 100644
--- a/ntp.conf
+++ b/ntp.conf
@@ -1 +1 @@
-NTP configuration
+NTP configuration - changed at feature branch
[root@gitbash demogit]# 
[root@gitbash demogit]# git checkout main
D       java.txt
D       network.txt
D       ref.txt
D       test.txt
Switched to branch 'main'
[root@gitbash demogit]# 
[root@gitbash demogit]# git diff main feature-linux
diff --git a/ntp.conf b/ntp.conf
index e626b9f..d1692ab 100644
--- a/ntp.conf
+++ b/ntp.conf
@@ -1 +1 @@
-NTP configuration
+NTP configuration - changed at feature branch
[root@gitbash demogit]#
```
---

## 10. Compare a Specific File

You can compare a specific file between commits:

```bash
git diff <commit1> <commit2> -- 50-redhat.conf
```

### Example

```bash
[root@gitbash demogit]# git diff 5b8b60b ea14fff -- 50-redhat.conf
diff --git a/50-redhat.conf b/50-redhat.conf
index 354c4c9..66c7d4b 100644
--- a/50-redhat.conf
+++ b/50-redhat.conf
@@ -19,4 +19,4 @@ X11Forwarding yes
 # It is recommended to use pam_motd in /etc/pam.d/sshd instead of PrintMotd,
 # as it is more configurable and versatile than the built-in version.
 PrintMotd no
-PermitRootLogin no
+PermitRootLogin yes
[root@gitbash demogit]# 
```

### Use Case

Useful when you only want to review changes to one file.

---

# Viewing Commit Statistics

## 11. `git show --stat`

Displays a summary of files changed by a commit.

### Command

```bash
git show --stat HEAD
```

### Example Output

```text
[root@gitbash demogit]# git show --stat HEAD
commit 1498157e8233f5c8ec4ea29cbabb7f46d1b0f755 (HEAD -> main, feature-linux)
Author: Arul C <salemarul1991@gmail.com>
Date:   Wed Sep 23 10:27:37 2026 +0000

    NTP at feature branch

 ntp.conf | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
[root@gitbash demogit]# 
```

### Use Case

Useful for getting a quick overview without displaying the complete diff.

---

# Viewing the Current Commit

## 12. `git rev-parse HEAD`

Displays the full commit ID of the current `HEAD`.

### Command

```bash
git rev-parse HEAD
```

### Example Output

```text
[root@gitbash demogit]# git rev-parse HEAD
1498157e8233f5c8ec4ea29cbabb7f46d1b0f755
[root@gitbash demogit]# 
```

### Use Case

Useful when you need the exact commit identifier for troubleshooting or comparison.

---


# Git Review Workflow

A typical workflow is:

```text
Make Changes
     |
     v
git diff
     |
     v
Review Changes
     |
     v
git add .
     |
     v
git diff --staged
     |
     v
Review Staged Changes
     |
     v
git commit
     |
     v
git log
     |
     v
git push
```

---

# Git Log and Diff Commands Summary

| Command                           | Purpose                             |
| --------------------------------- | ----------------------------------- |
| `git log`                         | View commit history                 |
| `git log --oneline`               | View compact commit history         |
| `git log --oneline --graph --all` | View commit and branch history      |
| `git show <commit>`               | Inspect a specific commit           |
| `git diff`                        | View unstaged changes               |
| `git diff --staged`               | View staged changes                 |
| `git diff HEAD`                   | Compare current changes with `HEAD` |
| `git diff A B`                    | Compare two commits                 |
| `git diff main feature`           | Compare two branches                |
| `git show --stat HEAD`            | View commit statistics              |
| `git rev-parse HEAD`              | Display current commit ID           |

---

# Key Takeaways

Git log and diff commands help infrastructure engineers:

* Review configuration changes
* Track infrastructure history
* Compare different versions
* Review changes before committing
* Investigate previous commits
* Understand branch history
* Maintain change traceability
* Support troubleshooting and rollback investigations

These commands are especially useful when managing Linux scripts, configuration files, Ansible playbooks, Dockerfiles, Kubernetes manifests, Terraform code, and cloud infrastructure code.
