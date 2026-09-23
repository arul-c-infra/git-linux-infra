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
git push
```

If the local branch is already connected to a remote branch, this is enough.

---

## 2. First Push

For a new branch, use:

```bash
git push -u origin main
```

Here:

* `git push` → Upload commits
* `origin` → Remote repository name
* `main` → Local branch
* `-u` → Set upstream tracking

After setting the upstream, you can usually use:

```bash
git push
```

---

## 3. Push a Specific Branch

Suppose you have:

```bash
git branch
```

Output:

```text
* linux-patching
  main
```

Push the branch:

```bash
git push -u origin linux-patching
```

This creates the remote branch:

```te
```
