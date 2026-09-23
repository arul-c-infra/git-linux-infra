# Git Merge and Rebase

## Overview

`git merge` and `git rebase` are used to integrate changes from one branch into another.

They are commonly used when working with feature branches, bug fixes, infrastructure changes, and team-based development.

---

# 1. Git Merge

`git merge` combines the changes from one branch into another branch.

For example:

```bash
git switch main
git merge feature-branch
```

This integrates `feature-branch` into `main`.

### Basic workflow

```text
main
  |
  A---B
       \
        C---D    feature-branch
```

After merge:

```text
main
  |
  A---B-------M
       \     /
        C---D
```

`M` is the merge commit.

---

# 2. Fast-Forward Merge

A fast-forward merge happens when the target branch has not changed after the feature branch was created.

Before merge:

```text
A---B---C
     \
      D---E
```

If `main` is at `C` and the feature branch contains `D` and `E`, Git can simply move the `main` pointer forward.

```text
A---B---C---D---E
```

### Example

```bash
git switch main
git merge feature-branch
```

Git may display:

```text
Fast-forward
```

No additional merge commit is required.

---

# 3. Three-Way Merge

A three-way merge is required when both branches contain new commits.

Example:

```text
A---B---C---D     main
     \
      E---F       feature-branch
```

After merging:

```text
A---B---C---D---M
     \         /
      E-------F
```

Git creates a merge commit `M`.

### Example

```bash
git switch main
git merge feature-branch
```

---

# 4. Typical Merge Workflow

A common feature development workflow is:

```bash
git switch main

git pull

git switch -c feature-monitoring

# Make changes

git status

git add .

git commit -m "Add monitoring configuration"

git switch main

git pull

git merge feature-monitoring

git push origin main
```

This workflow is useful when changes are developed separately and then integrated into `main`.

---

# 5. Merge Conflict

A merge conflict occurs when Git cannot automatically combine changes.

For example, two branches may modify the same line in a file.

```text
main:
server_port=8080

feature-branch:
server_port=9090
```

Git cannot automatically decide which value should be used.

You may see:

```text
CONFLICT (content): Merge conflict in config.txt
Automatic merge failed; fix conflicts and then commit the result.
```

---

# 6. Check Merge Conflict

Run:

```bash
git status
```

Example:

```text
You have unmerged paths.

Unmerged paths:
  both modified: config.txt
```

Open the conflicting file.

Git adds conflict markers:

```text
<<<<<<< HEAD
server_port=8080
=======
server_port=9090
>>>>>>> feature-branch
```

Meaning:

```text
<<<<<<< HEAD
```

Changes from the current branch.

```text
=======
```

Separates the two versions.

```text
>>>>>>> feature-branch
```

Changes from the branch being merged.

---

# 7. Resolve a Merge Conflict

Edit the file and keep the required configuration.

For example:

```text
server_port=9090
```

Remove all conflict markers.

Then:

```bash
git add config.txt
```

Check the status:

```bash
git status
```

Complete the merge:

```bash
git commit
```

Or provide the message directly:

```bash
git commit -m "Resolve merge conflict"
```

Then push:

```bash
git push origin main
```

---

# 8. Abort a Merge

If you do not want to continue with the merge:

```bash
git merge --abort
```

This attempts to return the repository to the state before the merge started.

Check:

```bash
git status
```

---

# 9. Git Rebase

`git rebase` moves or replays commits from one branch onto another base.

Example:

```bash
git switch feature-branch
git rebase main
```

Git takes the commits from `feature-branch` and replays them on top of the latest `main`.

Before rebase:

```text
A---B---C---D    main
     \
      E---F      feature-branch
```

After:

```text
A---B---C---D---E'---F'
```

`E'` and `F'` are new commits created by the rebase process.

---

# 10. Why Use Rebase?

Rebase can create a more linear project history.

Example:

```text
A---B---C---D---E---F
```

Instead of a history containing multiple merge branches.

This can make the commit history easier to follow.

However, rebase rewrites commit history, so it should be used carefully.

---

# 11. Basic Rebase Workflow

Update `main` first:

```bash
git switch main
git pull
```

Switch to the feature branch:

```bash
git switch feature-branch
```

Rebase onto `main`:

```bash
git rebase main
```

If there are no conflicts, the rebase completes automatically.

Check the history:

```bash
git log --oneline --graph --all
```

---

# 12. Rebase Conflict

A rebase can also produce conflicts.

Example:

```text
CONFLICT (content): Merge conflict in config.txt
```

Check:

```bash
git status
```

Edit the conflicting file and remove the conflict markers.

Then:

```bash
git add config.txt
```

Continue the rebase:

```bash
git rebase --continue
```

If additional conflicts occur, repeat the process:

```bash
git status
git add <file>
git rebase --continue
```

---

# 13. Abort a Rebase

If you want to cancel the rebase:

```bash
git rebase --abort
```

This attempts to restore the branch to its state before the rebase started.

---

# 14. Skip a Commit During Rebase

In specific situations, a commit may not be required.

You can skip the current commit with:

```bash
git rebase --skip
```

Use this only when you understand why the commit can be skipped.

---

# 15. Merge vs Rebase

| Feature           | Merge                          | Rebase                           |
| ----------------- | ------------------------------ | -------------------------------- |
| Purpose           | Integrate branches             | Replay commits onto another base |
| History           | Preserves branch structure     | Creates a more linear history    |
| Merge commit      | May create one                 | Normally does not                |
| Commit IDs        | Existing commits are preserved | Replayed commits get new IDs     |
| Conflict handling | Resolve during merge           | Resolve during rebase            |
| History rewriting | No                             | Yes                              |
| Shared commits    | Generally safer                | Requires more care               |

Neither command is universally required. The appropriate choice depends on the team's Git workflow.

---

# 16. Important Rebase Warning

Rebase changes commit history.

Avoid rebasing commits that other team members are already using unless the team workflow explicitly allows it.

For example:

```bash
git rebase main
```

can change the commit IDs of the feature branch.

If the branch has already been pushed and needs to be updated after a rebase, Git may require a force push.

If a force push is explicitly required, prefer:

```bash
git push --force-with-lease
```

over:

```bash
git push --force
```

`--force-with-lease` provides an additional check before replacing the remote branch.

For beginners, avoid force-pushing until the effects of history rewriting are understood.

---

# 17. Practical Linux Infrastructure Example

Suppose you maintain Linux infrastructure documentation.

You create a feature branch:

```bash
git switch -c feature-patching
```

Add patching documentation:

```text
linux-administration/
└── patching.md
```

Commit the changes:

```bash
git add patching.md
git commit -m "Add Linux patching documentation"
```

Meanwhile, another administrator updates `main`.

You can update your feature branch using rebase:

```bash
git switch main
git pull

git switch feature-patching
git rebase main
```

After successful testing, switch to `main`:

```bash
git switch main
```

Merge the feature:

```bash
git merge feature-patching
```

Push the changes:

```bash
git push origin main
```

---

# 18. Useful Commands

### Merge

```bash
git merge <branch>
```

### Abort merge

```bash
git merge --abort
```

### Rebase

```bash
git rebase <branch>
```

### Continue rebase

```bash
git rebase --continue
```

### Abort rebase

```bash
git rebase --abort
```

### Skip current rebase commit

```bash
git rebase --skip
```

### View branch history

```bash
git log --oneline --graph --all
```

### Check conflicts

```bash
git status
```

---

# 19. Recommended Workflow

For a typical infrastructure project:

```text
Create feature branch
        |
        v
Make changes
        |
        v
git add
        |
        v
git commit
        |
        v
Update from main
        |
        v
Merge or rebase
        |
        v
Test changes
        |
        v
Push changes
```

---

# 20. Key Points

* `git merge` combines branches.
* A fast-forward merge does not require a merge commit.
* A three-way merge may create a merge commit.
* Merge conflicts occur when Git cannot automatically combine changes.
* `git merge --abort` cancels an unfinished merge.
* `git rebase` replays commits on top of another branch.
* Rebase can create a linear project history.
* Rebase rewrites commit history and therefore requires care.
* `git rebase --continue` continues a rebase after resolving conflicts.
* `git rebase --abort` cancels an unfinished rebase.
* Avoid unnecessary force pushes after rebasing shared branches.
* Always test infrastructure changes before merging them into `main`.

