# Git Configuration Guide

Git configuration controls user identity, default behavior, and repository settings.

## 1. Check Git Version

```bash
git --version
```
**Output:**

**At Windows Git Bash**

Arul@LAPTOP-6CH5NSP0 MINGW64 ~
$ git --version
git version 2.55.0.windows.3

**At Linux:**

```bash
[root@gitbash ec2-user]# yum install git
Last metadata expiration check: 23:29:57 ago on Tue Sep 22 09:09:29 2026.
Dependencies resolved.
======================================================================================================================================================================
 Package                                  Architecture                   Version                                            Repository                           Size
======================================================================================================================================================================
Installing:
 git                                      x86_64                         2.50.1-1.amzn2023.0.1                              amazonlinux                          53 k
Installing dependencies:
 git-core                                 x86_64                         2.50.1-1.amzn2023.0.1                              amazonlinux                         4.9 M
 git-core-doc                             noarch                         2.50.1-1.amzn2023.0.1                              amazonlinux                         2.8 M
 perl-Error                               noarch                         1:0.17030-2.amzn2023.0.1                           amazonlinux                          42 k
 perl-File-Find                           noarch                         1.37-477.amzn2023.0.9                              amazonlinux                          26 k
 perl-Git                                 noarch                         2.50.1-1.amzn2023.0.1                              amazonlinux                          41 k
 perl-TermReadKey                         x86_64                         2.38-9.amzn2023.0.3                                amazonlinux                          36 k
 perl-lib                                 x86_64                         0.65-477.amzn2023.0.9                              amazonlinux                          15 k

Transaction Summary
======================================================================================================================================================================
Install  8 Packages

Total download size: 7.9 M
Installed size: 41 M
Is this ok [y/N]: y
Downloading Packages:
(1/8): git-2.50.1-1.amzn2023.0.1.x86_64.rpm                                                                                           2.0 MB/s |  53 kB     00:00    
(2/8): git-core-doc-2.50.1-1.amzn2023.0.1.noarch.rpm                                                                                   57 MB/s | 2.8 MB     00:00    
(3/8): perl-Error-0.17030-2.amzn2023.0.1.noarch.rpm                                                                                   1.4 MB/s |  42 kB     00:00    
(4/8): git-core-2.50.1-1.amzn2023.0.1.x86_64.rpm                                                                                       56 MB/s | 4.9 MB     00:00    
(5/8): perl-File-Find-1.37-477.amzn2023.0.9.noarch.rpm                                                                                642 kB/s |  26 kB     00:00    
(6/8): perl-Git-2.50.1-1.amzn2023.0.1.noarch.rpm                                                                                      1.0 MB/s |  41 kB     00:00    
(7/8): perl-TermReadKey-2.38-9.amzn2023.0.3.x86_64.rpm                                                                                1.3 MB/s |  36 kB     00:00    
(8/8): perl-lib-0.65-477.amzn2023.0.9.x86_64.rpm                                                                                      553 kB/s |  15 kB     00:00    
----------------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                                  44 MB/s | 7.9 MB     00:00     
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                                                              1/1 
  Installing       : git-core-2.50.1-1.amzn2023.0.1.x86_64                                                                                                        1/8 
  Installing       : git-core-doc-2.50.1-1.amzn2023.0.1.noarch                                                                                                    2/8 
  Installing       : perl-lib-0.65-477.amzn2023.0.9.x86_64                                                                                                        3/8 
  Installing       : perl-TermReadKey-2.38-9.amzn2023.0.3.x86_64                                                                                                  4/8 
  Installing       : perl-File-Find-1.37-477.amzn2023.0.9.noarch                                                                                                  5/8 
  Installing       : perl-Error-1:0.17030-2.amzn2023.0.1.noarch                                                                                                   6/8 
  Installing       : perl-Git-2.50.1-1.amzn2023.0.1.noarch                                                                                                        7/8 
  Installing       : git-2.50.1-1.amzn2023.0.1.x86_64                                                                                                             8/8 
  Running scriptlet: git-2.50.1-1.amzn2023.0.1.x86_64                                                                                                             8/8 
  Verifying        : git-2.50.1-1.amzn2023.0.1.x86_64                                                                                                             1/8 
  Verifying        : git-core-2.50.1-1.amzn2023.0.1.x86_64                                                                                                        2/8 
  Verifying        : git-core-doc-2.50.1-1.amzn2023.0.1.noarch                                                                                                    3/8 
  Verifying        : perl-Error-1:0.17030-2.amzn2023.0.1.noarch                                                                                                   4/8 
  Verifying        : perl-File-Find-1.37-477.amzn2023.0.9.noarch                                                                                                  5/8 
  Verifying        : perl-Git-2.50.1-1.amzn2023.0.1.noarch                                                                                                        6/8 
  Verifying        : perl-TermReadKey-2.38-9.amzn2023.0.3.x86_64                                                                                                  7/8 
  Verifying        : perl-lib-0.65-477.amzn2023.0.9.x86_64                                                                                                        8/8 

Installed:
  git-2.50.1-1.amzn2023.0.1.x86_64                       git-core-2.50.1-1.amzn2023.0.1.x86_64                  git-core-doc-2.50.1-1.amzn2023.0.1.noarch           
  perl-Error-1:0.17030-2.amzn2023.0.1.noarch             perl-File-Find-1.37-477.amzn2023.0.9.noarch            perl-Git-2.50.1-1.amzn2023.0.1.noarch               
  perl-TermReadKey-2.38-9.amzn2023.0.3.x86_64            perl-lib-0.65-477.amzn2023.0.9.x86_64                 

Complete!
[root@gitbash ec2-user]# 
[root@gitbash ec2-user]# 
[root@gitbash ec2-user]# git --version
git version 2.50.1
[root@gitbash ec2-user]# 
```


---

## 2. Configure User Name

Set the username globally:

```bash
git config --global user.name "Arul C"
```

**Verify:**

```bash
git config --global user.name
```
**Output:**
```bash
[root@gitbash ec2-user]# git config --global user.name "Arul C"
[root@gitbash ec2-user]# 
[root@gitbash ec2-user]# git config --global user.name
Arul C
[root@gitbash ec2-user]#
```
---

## 3. Configure Email

Set the email address globally:

```bash
git config --global user.email "your-email@example.com"
```

Verify:

```bash
git config --global user.email
```

> Use the email address associated with your GitHub account when appropriate.

---

## 4. View Global Configuration

```bash
git config --global --list
```

Example:

```text
user.name=Arul C
user.email=your-email@example.com
```

---

## 5. View All Configuration

```bash
git config --list
```

This displays configuration values from the applicable Git configuration levels.

---

## 6. Configuration Levels

Git supports different configuration scopes.

### System

Applies to all users on the system:

```bash
git config --system
```

### Global

Applies to the current user:

```bash
git config --global
```

### Local

Applies only to the current repository:

```bash
git config --local
```

The local repository configuration takes precedence over the global configuration.

---

## 7. Set Default Branch Name

Configure Git to use `main` as the default initial branch:

```bash
git config --global init.defaultBranch main
```

Verify:

```bash
git config --global init.defaultBranch
```

---

## 8. Configure Git Editor

For example, configure Vim:

```bash
git config --global core.editor "vim"
```

Or configure VS Code:

```bash
git config --global core.editor "code --wait"
```

---

## 9. Useful Configuration Commands

### List configuration

```bash
git config --list
```

### Get a specific value

```bash
git config user.name
```

### Remove a configuration value

```bash
git config --global --unset user.name
```

### Edit the global configuration file

```bash
git config --global --edit
```

---

## 10. Configuration File

The global Git configuration is commonly stored in:

```text
~/.gitconfig
```

View it:

```bash
cat ~/.gitconfig
```

---

## 11. Linux Infrastructure Example

Git configuration is important when Linux administrators maintain:

* Shell scripts
* Ansible playbooks
* Dockerfiles
* Kubernetes manifests
* Terraform files
* CloudFormation templates
* Infrastructure documentation

Example:

```bash
git config --global user.name "Arul C"
git config --global user.email "your-email@example.com"
git config --global init.defaultBranch main
```

Then verify:

```bash
git config --global --list
```

---

## Key Takeaways

| Configuration        | Purpose                                   |
| -------------------- | ----------------------------------------- |
| `user.name`          | Identifies the Git user                   |
| `user.email`         | Associates commits with an email          |
| `init.defaultBranch` | Sets the default initial branch           |
| `core.editor`        | Sets the Git text editor                  |
| `--global`           | Applies configuration to the current user |
| `--local`            | Applies configuration to one repository   |
| `--system`           | Applies configuration system-wide         |
