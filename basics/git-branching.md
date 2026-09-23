# Git Branching

Git branching allows developers and infrastructure engineers to work on different changes independently without affecting the main branch.

Branches are commonly used for:

* New features
* Bug fixes
* Configuration changes
* Infrastructure changes
* Testing
* Documentation updates

---

## 1. What is a Git Branch?

A branch is an independent line of development.

Example:

```text
main
  |
  A---B---C
           \
            D---E
             feature
```

The `main` branch contains the stable version.

The `feature` branch can be used to develop and test changes separately.

---

## 2. Check Current Branch

Use:

```bash
git branch
```

Example:

```text
* main
```

The `*` indicates the current branch.

Another option:

```bash
git status
```

Example:

```text
On branch main
```

---

## 3. Create a New Branch

Command:

```bash
git branch feature-linux-docs
```

Check branches:

```bash
git branch
```

Example:

```text
  feature-linux-docs
* main
```

The branch is created, but you are still on `main`.

---

## 4. Switch to a Branch

Command:

```bash
git switch feature-linux-docs
```

Example:

```text
Switched to branch 'feature-linux-docs'
```

Verify:

```bash
git branch
```

Output:

```text
* feature-linux-docs
  main
```

---

## 5. Create and Switch in One Command

Instead of using two commands:

```bash
git branch feature-linux-docs
git switch feature-linux-docs
```

You can use:

```bash
git switch -c feature-linux-docs
```

This creates the branch and switches to it.

---

## 6. Older Command: git checkout

The traditional command is:

```bash
git checkout -b feature-linux-docs
```

This also creates and switches to the branch.

Modern Git generally recommends `git switch` for switching branches because it is more specific and easier to understand.

---

##
