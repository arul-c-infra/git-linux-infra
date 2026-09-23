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
commit 2cc475c6959ddb856256d5f5d86e708fa6d3fa68
Author: Arul C
Date:   Wed Sep 23 2026

    Add Git commands reference

commit 39f556c37432fa56e227e5163b4d1a8b5e965519
Author: Arul C
Date:   Wed Sep 23 2026

    Update README.md
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
2cc475c Add Git commands reference
39f556c Update README.md
e28b9c6 Initial commit
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
* 2cc475c Add Git commands reference
* 39f556c Update README.md
* e28b9c6 Initial commit
```

When multiple branches exist, the graph can look like:

```text
*   7a12345 Merge feature branch
|\
| * 6b23456 Add Linux script
|/
* 2cc475c Add Git commands reference
* 39f556c Update README.md
```

### Use Case

Useful for understanding branch and merge history.

---

## 4. `git show`

Displays information about a specific commit.

### Command

```bash
git show <commit-id>
```

### Example

```bash
git show 2cc475c
```

### Example Output

```text
commit 2cc475c
Author: Arul C

    Add Git commands reference

diff --git a/basics/git-commands.md b/basics/git-commands.md
new file mode 100644
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
Linux Server
```

You change it to:

```text
Linux Infrastructure Server
```

Run:

```bash
git diff
```

### Example Output

```diff
- Linux Server
+ Linux Infrastructure Server
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
git add test.sh
```

Then:

```bash
git diff --staged
```

### Example Output

```diff
- echo "Linux Server"
+ echo "Linux Infrastructure Server"
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

### Use Case

Useful for reviewing all current changes against the latest committed version.

---

## 8. Compare Two Commits

You can compare two commits using:

```bash
git diff <commit1> <commit2>
```

### Example

```bash
git diff 39f556c 2cc475c
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

---

## 10. Compare a Specific File

You can compare a specific file between commits:

```bash
git diff <commit1> <commit2> -- README.md
```

### Example

```bash
git diff 39f556c 2cc475c -- README.md
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
commit 2cc475c

    Add Git commands reference

 basics/git-commands.md | 120 +++++++++++++++++++++
 1 file changed, 120 insertions(+)
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
2cc475c6959ddb856256d5f5d86e708fa6d3fa68
```

### Use Case

Useful when you need the exact commit identifier for troubleshooting or comparison.

---

# Practical Linux Infrastructure Example

Consider a Linux server configuration stored in Git.

Before a change:

```text
/etc/ssh/sshd_config
```

Suppose an administrator changes:

```text
PermitRootLogin no
```

to:

```text
PermitRootLogin prohibit-password
```

Before committing the change:

```bash
git diff
```

The administrator can review the change.

Then:

```bash
git add sshd_config
```

Review the staged change:

```bash
git diff --staged
```

Commit the change:

```bash
git commit -m "Update SSH root login configuration"
```

Later, the administrator can investigate the change using:

```bash
git log
```

or:

```bash
git show <commit-id>
```

This provides a history of infrastructure changes.

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
