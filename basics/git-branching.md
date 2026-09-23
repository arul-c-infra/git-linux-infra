# Git Branching

Git branching allows developers and infrastructure engineers to work on different changes independently without affecting the main branch.

**Branches are commonly used for:**

* New features
* Bug fixes
* Configuration changes
* Infrastructure changes
* Testing
* Documentation updates
---

## 1. What is a Git Branch?
A branch is an independent line of development.

**Example:**

```text
main
  |
  A---B---C
           \
            D---E
             feature
```

The **`main**` branch contains the stable version.

The `feature` branch can be used to develop and test changes separately.

---

## 2. Check Current Branch

```bash
git branch
```

**Example:**

```text
[root@gitbash branch]# git branch 
* main
[root@gitbash branch]# 
```
The `*` indicates the current branch.

**Another option**:
```bash
git status
```

**Output:**
```bash
[root@gitbash branch]# git status
On branch main
nothing to commit, working tree clean
[root@gitbash branch]# 
```
---

## 3. Create a New Branch

**Command:**
```bash
git branch feature-linux-docs
```

**Check branches:**

```bash
git branch
```

**Output:**
```bash
 [root@gitbash branch]# git branch feature-linux-docs
[root@gitbash branch]# 
[root@gitbash branch]# git branch
  feature-linux-docs
* main
[root@gitbash branch]# 
```
```test
The branch is created, but you are still on `main`.
```
---

## 4. Switch to a Branch

**Command:**
```bash
git switch feature-linux-docs
```

**output:**
```bash
[root@gitbash branch]# git switch feature-linux-docs 
Switched to branch 'feature-linux-docs'
[root@gitbash branch]# 
[root@gitbash branch]# git branch
* feature-linux-docs
  main
[root@gitbash branch]# 
```
---

## 5. Create and Switch in One Command

**Instead of using two commands:**

```bash
git branch feature-linux-docs2
git switch feature-linux-docs2
```
**Example:**

```bash
[root@gitbash branch]# git branch feature-linux-docs2
[root@gitbash branch]# 
[root@gitbash branch]# git switch feature-linux-docs2
Switched to branch 'feature-linux-docs2'
[root@gitbash branch]# 
[root@gitbash branch]# git branch 
  feature-linux-docs
  feature-linux-docs1
* feature-linux-docs2
  main
[root@gitbash branch]# 
```
```test
This creates the branch and switches to it.
```
---

## 6. Older Command: git checkout

The traditional command is:

```bash
git checkout -b feature-linux-docs1
```

This also creates and switches to the branch.

Modern Git generally recommends `git switch` for switching branches because it is more specific and easier to understand.

**Output:**
```bash
[root@gitbash branch]# git checkout -b feature-linux-docs1
Switched to a new branch 'feature-linux-docs1'
[root@gitbash branch]# 
[root@gitbash branch]# git branch 
  feature-linux-docs
*** feature-linux-docs1**
  main
[root@gitbash branch]# 
```
---

## 7. Work on a Feature Branch

**After switching to the branch:**

```bash
   git switch feature-linux-docs
```
**Create or modify a file:**
```bash
echo "Linux patching process" > patching.md
```
**Check the status:**

```bash
git status
```
**Stage the file:**
```bash
git add patching.md
```
**Commit the change:**
```bash
git commit -m "Add Linux patching documentation"
```
The commit is now part of the feature-linux-docs branch.

```bash
[root@gitbash branch]# git switch feature-linux-docs
Switched to branch 'feature-linux-docs'
[root@gitbash branch]# 
[root@gitbash branch]# echo "Linux patching process" > patching.md
[root@gitbash branch]# 
[root@gitbash branch]# git status
On branch feature-linux-docs
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        patching.md

nothing added to commit but untracked files present (use "git add" to track)
[root@gitbash branch]# 
[root@gitbash branch]# git add patching.md 
[root@gitbash branch]# 
[root@gitbash branch]# git commit -m "Add Linux patching documentation"
[feature-linux-docs b5202a6] Add Linux patching documentation
 1 file changed, 1 insertion(+)
 create mode 100644 patching.md
[root@gitbash branch]# 
```
---
## 8. View Branches
Local branches
```bash
git branch
```

Remote branches
```bash
git branch -r
```

All branches
```bash
git branch -a
```
Example:

```bash
[root@gitbash branch]# git branch -a
  feature-linux-docs
  feature-linux-docs1
  feature-linux-docs2
* main
[root@gitbash branch]# 
```
---
## 9. Switch Back to Main

**Command:**
```bash
git switch main
git status
```

**Example:**
```bash
[root@gitbash branch]# git switch main
Switched to branch 'main'
[root@gitbash branch]# 
[root@gitbash branch]# git status
On branch main
nothing to commit, working tree clean
[root@gitbash branch]# 
[root@gitbash branch]#
```
---
## 10. Merge a Branch

After completing and testing the changes, you can merge the feature branch into main.

**First switch to main:**
```bash
git switch main
```

**Then merge:**
```bash
git merge feature-linux-docs
```
**Example:**
```bash
[root@gitbash branch]# 
[root@gitbash branch]# git switch main 
Switched to branch 'main'
[root@gitbash branch]# 
[root@gitbash branch]# git merge feature-linux-docs
Updating a306c5e..e2677d6
Fast-forward
 patching.md | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 patching.md
[root@gitbash branch]#
```

The changes from feature-linux-docs are now included in main.
---
**11. Delete a Branch**

After merging the branch, it can be deleted.
```bash
git branch -d feature-linux-docs
```
**Example:**
```bash
[root@gitbash branch]# git branch -d feature-linux-docs
Deleted branch feature-linux-docs (was e2677d6).
[root@gitbash branch]#
[root@gitbash branch]# git branch 
  feature-linux-docs1
  feature-linux-docs2
* main
[root@gitbash branch]# 
```
---
## 12. Rename a Branch

**Rename the current branch:**
```bash
git branch -m new-branch-name
```

**Example:**
```bash
[root@gitbash branch]# git branch 
* feature-linux-docs1
  feature-linux-docs2
  main
[root@gitbash branch]# 
[root@gitbash branch]# git branch -m feature-linux-modifed
[root@gitbash branch]# 
[root@gitbash branch]# git branch 
  feature-linux-docs2
* feature-linux-modifed
  main
[root@gitbash branch]#
```
---
## 13. Compare Branches

To see commits that exist in one branch but not another:

```bash
 agit log main..feature-linux-docs
```
To compare the actual file changes:
```bash
git diff main..feature-linux-docs
```
**Example:**

```bash
[root@gitbash branch]# git log main..feature-linux-modifed
commit 7d47643e707d5e232fe9ae2bc6cfd99965528284 (feature-linux-modifed)
Author: arul <salemarul1991@gmail.com>
Date:   Wed Sep 23 11:59:23 2026 +0000

    changed at feature branch
[root@gitbash branch]#
```

This is useful before merging infrastructure changes.
---
## 14. Practical Linux Infrastructure Example

Imagine the main branch contains stable Linux administration documentation.

main
 |
 A---B---C

You need to add a new patching procedure.

Create a branch:

```bash
git switch -c linux-patching
```

Make changes:
```bash
vim patching.md
```
Check:
```bash
git status
```
Stage:
```bash
git add patching.md
```
Commit:
```bash
git commit -m "Add Linux patching procedure"
```
Now the history looks like:

```text
main
 |
 A---B---C
          \
           D
            \
          linux-patching
```

After testing the documentation:
```bash
git switch main
git merge linux-patching
```
Now the change is included in main.

---
## 15. Branching Workflow

A common workflow is:

main
  |
  | git switch -c feature-name
  ↓
feature branch
  |
  | Make changes
  ↓
git add
  |
  ↓
git commit
  |
  ↓
Test / Review
  |
  ↓
git switch main
  |
  ↓
git merge feature-name
  |
  ↓
main

---
## 16. Branch Naming Examples

Use meaningful branch names.

Linux
linux-patching
linux-security-update
linux-monitoring
linux-user-management
AWS
aws-ec2-project
aws-iam-update
aws-networking
Docker
docker-networking
docker-volume
docker-security
Documentation
update-readme
add-git-documentation
fix-documentation

Avoid unclear names such as:

test
new
branch1
abc
mybranch
17. Useful Branch Commands
Command	Purpose
git branch	List local branches
git branch <name>	Create a branch
git switch <name>	Switch branches
git switch -c <name>	Create and switch
git branch -a	List all branches
git branch -r	List remote branches
git merge <name>	Merge a branch
git branch -d <name>	Delete a branch
git branch -m <name>	Rename a branch
git diff main..branch	Compare branches
git log main..branch	Compare commit history
18. Important Points
Branches do not create a completely separate repository

Branches share the same Git repository and commit history.

Always check your current branch

Before making important changes:

git status

or:

git branch
Use meaningful branch names

A good branch name makes it easier for administrators and team members to understand the purpose of the change.

Test before merging

For infrastructure work:

Create branch
    ↓
Make change
    ↓
Commit
    ↓
Test
    ↓
Review
    ↓
Merge into main
Key Takeaways

The most important branching commands are:

git branch
git switch -c feature-name
git switch main
git merge feature-name
git branch -d feature-name

A simple Git branching model is:

main
  |
  +---- feature branch
  |          |
  |       changes
  |          |
  |       commits
  |          |
  +------ merge
             |
            main

For Linux infrastructure administration, branches help isolate changes before they are merged into the stable main branch.
