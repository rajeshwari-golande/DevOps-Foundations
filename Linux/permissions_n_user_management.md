# Linux Day 3 — Permissions, Ownership, and User Management

> **Goal:** Understand Linux permissions and users for DevOps, Cloud, MLOps, and technical interviews.

## Table of Contents
1. [Learning Goals](#1-learning-goals)
2. [Users, Groups, and Permissions](#2-users-groups-and-permissions)
3. [`ls -l`](#3-ls--l--read-permissions)
4. [`whoami`](#4-whoami--current-user)
5. [`id`](#5-id--user-and-group-ids)
6. [`groups`](#6-groups--group-membership)
7. [`chmod`](#7-chmod--change-permissions)
8. [`chown`](#8-chown--change-ownership)
9. [`chgrp`](#9-chgrp--change-group-ownership)
10. [`umask`](#10-umask--default-permissions)
11. [`sudo`](#11-sudo--elevated-privileges)
12. [`su`](#12-su--switch-user)
13. [`passwd`](#13-passwd--manage-passwords)
14. [File vs Directory Permissions](#14-file-vs-directory-permissions)
15. [Common Permission Modes](#15-common-permission-modes)
16. [Troubleshooting](#16-troubleshooting-permission-denied)
17. [Hands-on Lab](#17-safe-hands-on-lab)
18. [Interview Questions](#18-interview-questions)
19. [Cheat Sheet](#19-quick-reference-cheat-sheet)
20. [Completion Checklist](#20-day-3-completion-checklist)

---

## 1. Learning Goals

By the end, you should be able to:
- Read permissions shown by `ls -l`.
- Explain read (`r`), write (`w`), and execute (`x`).
- Distinguish owner, group, and other users.
- Change permissions using numeric and symbolic `chmod`.
- Explain `chown`, `chgrp`, and `umask`.
- Check your user and groups with `whoami`, `id`, and `groups`.
- Explain `sudo` versus `su`.
- Investigate a basic `Permission denied` error safely.

> **Safety:** Practice in a directory you own. Avoid changing permissions recursively on system directories or using `chmod -R 777` as a fix.

## 2. Users, Groups, and Permissions

Linux uses permissions to control access to files and directories.

| Class | Meaning |
|---|---|
| Owner (`u`) | The user who owns the file |
| Group (`g`) | Users associated with the file's group |
| Others (`o`) | Everyone else |

| Permission | Symbol | Value | On a file | On a directory |
|---|---|---:|---|---|
| Read | `r` | 4 | Read contents | List names |
| Write | `w` | 2 | Modify contents | Create/remove/rename entries, subject to other checks |
| Execute | `x` | 1 | Run as a program/script, if valid | Traverse/access entries by path |

## 3. `ls -l` — Read Permissions

```bash
ls -l
```

Example:

```text
-rwxr-xr-- 1 rajeshwari developers 1200 Oct 9 10:00 deploy.sh
```

Breakdown:

```text
- rwx r-x r--
│  │   │   └── Others: read
│  │   └────── Group: read + execute
│  └────────── Owner: read + write + execute
└───────────── File type
```

The first character identifies the type:
- `-` = regular file
- `d` = directory
- `l` = symbolic link

The next nine characters are three permission groups: owner, group, others.

Useful variations:

```bash
ls -l file.txt     # Details for one file
ls -la             # Include hidden entries
ls -ld myfolder    # Show the directory itself
```

## 4. `whoami` — Current User

Prints the current effective username:

```bash
whoami
```

Example output:

```text
rajeshwari
```

Use this to check which account your terminal is using.

## 5. `id` — User and Group IDs

```bash
id
```

Example output:

```text
uid=1000(rajeshwari) gid=1000(rajeshwari) groups=1000(rajeshwari),27(sudo)
```

- `uid` = user ID
- `gid` = primary group ID
- `groups` = supplementary groups and group memberships

Check another account:

```bash
id username
```

Permissions can depend on numeric IDs and group membership, not just the username.

## 6. `groups` — Group Membership

Show the current user's groups:

```bash
groups
```

Check another user:

```bash
groups username
```

Groups let teams share access without making every team member the owner. After group membership changes, you may need a new login session for the change to appear in your current shell.

## 7. `chmod` — Change Permissions

`chmod` means **change mode**. It changes a file or directory's permission bits.

### 7.1 Numeric permissions

Remember:

```text
r = 4
w = 2
x = 1
```

Add values for each class:

| Number | Permissions | Calculation |
|---:|---|---|
| `0` | `---` | 0 |
| `1` | `--x` | 1 |
| `2` | `-w-` | 2 |
| `3` | `-wx` | 2 + 1 |
| `4` | `r--` | 4 |
| `5` | `r-x` | 4 + 1 |
| `6` | `rw-` | 4 + 2 |
| `7` | `rwx` | 4 + 2 + 1 |

Three digits mean **owner, group, others**, in that order.

Example:

```bash
chmod 755 script.sh
```

`755` means:
- Owner: `7` = `rwx`
- Group: `5` = `r-x`
- Others: `5` = `r-x`

Result: `rwxr-xr-x`

Another example:

```bash
chmod 644 notes.txt
```

`644` means owner gets read/write; group and others get read-only access. Result: `rw-r--r--`.

### 7.2 Symbolic permissions

Symbols:
- `u` = owner
- `g` = group
- `o` = others
- `a` = all classes
- `+` = add permissions
- `-` = remove permissions
- `=` = set permissions exactly for selected classes

Examples:

```bash
chmod u+x script.sh     # Add execute for owner
chmod g-w file.txt      # Remove group write
chmod o-r file.txt      # Remove others' read
chmod a+r file.txt      # Add read for everyone
chmod u=rw,go=r file.txt
```

The last command sets owner to read/write and group/others to read only.

### 7.3 Options and cautions

```bash
chmod -v 644 notes.txt
```

`-v` prints a message for processed files.

```bash
chmod -R 755 directory/
```

`-R` applies recursively. Use it carefully: files and directories often need different permissions.

Avoid using `chmod 777` as a routine fix. It grants everyone read, write, and execute access and can expose data or allow unauthorized changes.

### Make a script executable

```bash
chmod u+x script.sh
./script.sh
```

The script must also have a valid interpreter or executable format, and the filesystem must allow execution.

## 8. `chown` — Change Ownership

`chown` means **change owner**.

```bash
sudo chown alice report.txt
```

This changes the owner to `alice`. Changing ownership generally requires administrator privileges.

Change owner and group:

```bash
sudo chown alice:developers report.txt
```

Recursive change:

```bash
sudo chown -R alice:developers project/
```

Use `-R` only when intended; it affects the directory and its contents.

Verify:

```bash
ls -l report.txt
```

**Difference:** `chmod` changes permissions; `chown` changes ownership and can also set the group.

## 9. `chgrp` — Change Group Ownership

`chgrp` means **change group**.

```bash
sudo chgrp developers report.txt
```

This changes the file's group, assuming the group exists and you have sufficient permission.

Recursive change:

```bash
sudo chgrp -R developers project/
```

Verify with `ls -l`.

**Difference:** `chgrp` specifically changes the group; `chown` can change owner and group.

## 10. `umask` — Default Permissions

`umask` controls which permission bits are **masked out** when new files and directories are created.

Check it:

```bash
umask
```

A common value is `0022`.

For typical Linux creation modes:
- New files start from base mode `666` (no execute bits).
- New directories start from base mode `777`.

With umask `022`, this commonly results in:
- Files: `644`
- Directories: `755`

This is a bit-mask operation, not ordinary decimal subtraction. Applications may choose their own modes, so results can differ.

Set it for the current shell:

```bash
umask 027
```

Typical results are files `640` and directories `750`. This normally affects the current shell and child processes, not every user or the whole system permanently.

Safe test:

```bash
umask
touch umask-test.txt
mkdir umask-test-dir
ls -ld umask-test.txt umask-test-dir
```

## 11. `sudo` — Elevated Privileges

`sudo` runs a command with privileges allowed by the system's sudo policy, often as root.

```bash
sudo apt update
```

Some actions, such as installing packages or changing protected system files, require elevated privileges.

Best practices:
- Use `sudo` only when needed.
- Understand commands before running them with elevated privileges.
- Avoid running unknown scripts as root.
- Do not use `sudo` blindly to fix every `Permission denied` error.

Check your permitted sudo commands:

```bash
sudo -l
```

## 12. `su` — Switch User

`su` attempts to switch to another user:

```bash
su username
```

A login shell for that user:

```bash
su - username
```

Comparison:

| Command | Purpose |
|---|---|
| `sudo command` | Run one command with permitted elevated privileges |
| `sudo -i` | Start a root login shell, if permitted |
| `su username` | Switch to another user |
| `su - username` | Switch user with a login environment |

Prefer running only the command you need with `sudo` instead of staying in a root shell.

## 13. `passwd` — Manage Passwords

Change your own password:

```bash
passwd
```

An administrator may be able to set another user's password:

```bash
sudo passwd username
```

Behavior depends on system policy. Never put passwords in scripts, command history, screenshots, or GitHub repositories.

## 14. File vs Directory Permissions

| Permission | On a file | On a directory |
|---|---|---|
| `r` | Read contents | List names |
| `w` | Modify contents | Create/remove/rename entries, subject to other checks |
| `x` | Execute file | Traverse/access entries by path |

Important details:
- A directory may be readable but not traversable if it lacks `x`.
- A script may be readable but not executable.
- Deleting a file usually depends on permissions on its parent directory, not only the file's own write permission.
- Sticky bits and ACLs can add rules beyond basic permission bits.

## 15. Common Permission Modes

| Mode | Symbolic form | Common use |
|---:|---|---|
| `600` | `rw-------` | Private file for owner |
| `644` | `rw-r--r--` | Ordinary text/config file |
| `700` | `rwx------` | Private directory or executable |
| `755` | `rwxr-xr-x` | Executable or directory accessible to others |
| `750` | `rwxr-x---` | Owner full access, group access, no access for others |
| `640` | `rw-r-----` | Owner read/write, group read, others no access |

These are common patterns, not universal rules. Choose permissions based on the data and access requirements.

## 16. Troubleshooting `Permission denied`

Investigate instead of immediately changing permissions.

### Step 1 — Check your identity

```bash
whoami
id
groups
```

### Step 2 — Inspect the target and parent directory

```bash
ls -l file.txt
ls -ld parent_directory
```

For paths with multiple parent directories, inspect the relevant directory permissions too.

### Step 3 — Check what permission is needed

- Reading a file requires read permission and traversal permission on parent directories.
- Writing a file requires write permission and traversal permission on parent directories.
- Executing a script requires execute permission, a usable interpreter/format, and an execution-permitting filesystem.
- Listing a directory requires read permission; accessing entries by path generally requires execute permission.

### Step 4 — Make the smallest appropriate change

If you own a script and need to execute it:

```bash
chmod u+x script.sh
```

Do not default to:

```bash
chmod 777 script.sh
```

If a protected file belongs to another user, verify the intended ownership and system policy before changing anything.

## 17. Safe Hands-on Lab

Complete this in a directory you own, such as your home directory or WSL home.

### Task 1 — Create a practice directory

```bash
mkdir -p ~/linux-day3
cd ~/linux-day3
```

### Task 2 — Create a file and script

```bash
touch notes.txt
printf '#!/bin/sh\necho "Hello from Linux"\n' > hello.sh
```

### Task 3 — Inspect permissions

```bash
ls -l
```

Observe the permission bits for each file.

### Task 4 — Set text-file permissions

```bash
chmod 644 notes.txt
ls -l notes.txt
```

Expected symbolic permissions:

```text
-rw-r--r--
```

### Task 5 — Make the script executable by its owner

```bash
chmod u+x hello.sh
ls -l hello.sh
./hello.sh
```

Expected output:

```text
Hello from Linux
```

### Task 6 — Practice symbolic changes

```bash
chmod g-r notes.txt
ls -l notes.txt
chmod g+r notes.txt
```

The final command restores group read permission.

### Task 7 — Check identity and groups

```bash
whoami
id
groups
```

### Task 8 — Inspect umask

```bash
umask
touch another.txt
mkdir another-dir
ls -ld another.txt another-dir
```

### Task 9 — Inspect ownership

```bash
ls -l notes.txt hello.sh
```

You do not need to change ownership to complete this lab. Only practice `chown` or `chgrp` if you have a legitimate test user/group and understand the consequences.

## 18. Interview Questions

### Q1. Difference between `chmod` and `chown`?

`chmod` changes permissions; `chown` changes ownership and can also change the group.

### Q2. What does `chmod 755 script.sh` mean?

Owner gets read/write/execute; group and others get read/execute.

### Q3. What does `chmod 644 file.txt` mean?

Owner gets read/write; group and others get read-only access.

### Q4. What do `r`, `w`, and `x` mean?

For files: read, modify, execute. For directories: list names, modify directory entries, and traverse/access entries.

### Q5. What is `umask`?

It masks permission bits from the default modes used when new files and directories are created.

### Q6. Difference between `sudo` and `su`?

`sudo` runs commands under permitted elevated credentials; `su` switches to another user shell.

### Q7. How do you check your user ID and groups?

```bash
id
groups
```

### Q8. Why is `chmod 777` usually a bad idea?

It grants everyone read/write/execute permissions and can enable unauthorized access or changes.

### Q9. Why might you be unable to access a file even if it is readable?

You may lack execute/traverse permission on a parent directory.

### Q10. What does `ls -ld directory/` do?

It displays the directory's own metadata and permissions rather than listing its contents.

## 19. Quick Reference Cheat Sheet

```bash
# Detailed permissions and ownership
ls -l

# Show a directory itself
ls -ld directory/

# Current user
whoami

# UID, GID, and group memberships
id

# Group membership
groups

# Owner read/write; group and others read
chmod 644 file.txt

# Owner full access; group and others read/execute
chmod 755 script.sh

# Add execute for owner
chmod u+x script.sh

# Remove group write
chmod g-w file.txt

# Change owner (usually requires elevated privileges)
sudo chown username file.txt

# Change owner and group
sudo chown username:groupname file.txt

# Change group
sudo chgrp groupname file.txt

# Show current umask
umask

# Set umask for current shell
umask 027

# Run one command with elevated privileges
sudo command

# Start a login shell as another user
su - username

# Change your own password
passwd
```

## 20. Day 3 Completion Checklist

- [ ] I can interpret the nine permission characters in `ls -l`.
- [ ] I understand owner, group, and others.
- [ ] I can convert numeric permissions into symbolic permissions.
- [ ] I can use `chmod` safely.
- [ ] I understand `chown` and `chgrp`.
- [ ] I can check the current user with `whoami`.
- [ ] I can inspect user/group IDs with `id` and `groups`.
- [ ] I understand what `umask` does.
- [ ] I know when and why to use `sudo`.
- [ ] I understand `sudo` versus `su`.
- [ ] I can investigate a basic `Permission denied` error.
- [ ] I completed the safe hands-on lab.
- [ ] I can answer the interview questions without looking at the notes.

---

## Linux Learning Progress

### Day 1 — File and Directory Management

`pwd`, `ls`, `cd`, `mkdir`, `touch`, `cp`, `mv`, `rm`, `cat`, `find`

### Day 2 — Text Processing and Log Analysis

`grep`, `head`, `tail`, `less`, `wc`, `sort`, `uniq`, `cut`, `awk`, `sed`

**Still to complete from Day 2:** command pipelines, command comparison, remaining cheat sheet, and practical Linux/log-analysis exercises.

### Day 3 — Permissions and User Management

`ls -l`, `whoami`, `id`, `groups`, `chmod`, `chown`, `chgrp`, `umask`, `sudo`, `su`, `passwd`

### Suggested Next Topic

Linux process and system monitoring: `ps`, `top`, `htop`, `kill`, `killall`, `jobs`, `bg`, `fg`, `free`, `df`, `du`, and `uptime`.
