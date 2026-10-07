# Linux Day 1 — Essential Commands

> **Goal:** Build Linux fundamentals for Cloud/DevOps and FAANG interviews.  
> Focus on understanding what each command does, important options, and common interview use cases.

---

## 0. Linux Paths — Foundation

Linux has a single hierarchical filesystem starting at `/`.

```text
/
├── bin
├── boot
├── dev
├── etc
├── home
│   └── user
├── lib
├── opt
├── proc
├── root
├── tmp
├── usr
└── var
```

### Special paths

| Symbol | Meaning |
|---|---|
| `/` | Root of the entire filesystem |
| `~` | Current user's home directory |
| `.` | Current directory |
| `..` | Parent directory |
| `-` | Previous directory used by `cd` |

### Absolute path

Starts from `/` and uniquely identifies a location.

```bash
/home/user/projects/app.py
```

### Relative path

Starts from the current directory.

```bash
projects/app.py
./projects/app.py
../file.txt
```

---

# 1. `pwd` — Print Working Directory

## Purpose

Displays the directory you are currently working in.

### Syntax

```bash
pwd [OPTION]
```

### Basic usage

```bash
pwd
```

Example:

```text
/home/user/linux-practice
```

## Important options

### `-L` — Logical path

```bash
pwd -L
```

Shows the **logical path**, preserving symbolic links. This is generally the default behavior.

### `-P` — Physical path

```bash
pwd -P
```

Shows the **physical filesystem path**, resolving symbolic links.

### Example

If:

```text
/home/user/project -> /var/www/project
```

Then:

```bash
pwd -L
```

may show:

```text
/home/user/project
```

while:

```bash
pwd -P
```

shows:

```text
/var/www/project
```

## Interview point

**Q: Difference between `pwd -L` and `pwd -P`?**

```text
-L → logical path; preserves symbolic links
-P → physical path; resolves symbolic links
```

---

# 2. `ls` — List Directory Contents

## Purpose

Lists files and directories.

### Syntax

```bash
ls [OPTIONS] [PATH]
```

### Basic

```bash
ls
```

## Important options

### `-l` — Long format

```bash
ls -l
```

Typical output:

```text
-rw-r--r-- 1 user user 1234 Oct 2 file.txt
```

Shows:

```text
permissions
number of links
owner
group
size
modification time
name
```

Permissions will be covered separately.

### `-a` — All files

```bash
ls -a
```

Shows hidden files such as:

```text
.bashrc
.git
.env
```

Files beginning with `.` are generally hidden.

### `-h` — Human-readable sizes

```bash
ls -lh
```

Displays sizes such as:

```text
118M
2.4G
```

instead of raw byte counts.

### `-R` — Recursive

```bash
ls -R
```

Lists contents of directories recursively.

### `-t` — Sort by modification time

```bash
ls -lt
```

Newest modified files first.

### `-S` — Sort by size

```bash
ls -lS
```

Largest files first.

### Most useful combination

```bash
ls -lah
```

Meaning:

```text
-l → long format
-a → hidden files
-h → human-readable sizes
```

## Interview questions

**Show hidden files:**

```bash
ls -a
```

**Show detailed information including hidden files:**

```bash
ls -la
```

**Show files sorted by size:**

```bash
ls -lS
```

---

# 3. `cd` — Change Directory

## Purpose

Navigates between directories.

### Syntax

```bash
cd [DIRECTORY]
```

### Absolute path

```bash
cd /var/log
```

### Relative path

```bash
cd projects
```

### Parent directory

```bash
cd ..
```

### Home directory

```bash
cd ~
```

or simply:

```bash
cd
```

### Previous directory

```bash
cd -
```

Example:

```bash
cd /var/log
cd /tmp
cd -
```

The last command takes you back to `/var/log`.

## Important concepts

```text
/   → root
~   → home
.   → current directory
..  → parent directory
-   → previous directory
```

## Interview question

**Difference between `cd /` and `cd ~`?**

```text
cd / → root of the entire filesystem
cd ~ → current user's home directory
```

---

# 4. `mkdir` — Make Directory

## Purpose

Creates directories.

### Syntax

```bash
mkdir [OPTIONS] DIRECTORY
```

### Basic

```bash
mkdir projects
```

## Important options

### `-p` — Create parent directories

```bash
mkdir -p project/src/utils
```

Creates:

```text
project/
└── src/
    └── utils/
```

even when the parent directories don't exist.

### `-v` — Verbose

```bash
mkdir -v test
```

Displays what was created.

### `-m` — Set permissions

```bash
mkdir -m 755 project
```

Creates the directory with the specified permissions.

Permissions such as `755` will be covered later.

## Interview question

**Why use `mkdir -p`?**

It creates missing parent directories automatically.

---

# 5. `touch` — Create/Update File

## Purpose

`touch` updates a file's timestamps. If the file doesn't exist, it creates an empty file.

### Syntax

```bash
touch [OPTIONS] FILE
```

### Create a file

```bash
touch notes.txt
```

### Multiple files

```bash
touch a.txt b.txt c.txt
```

## Important concept

A common beginner explanation is:

> `touch` creates a file.

More accurately:

> `touch` updates file timestamps and creates the file if it doesn't already exist.

If:

```text
notes.txt
```

already exists:

```bash
touch notes.txt
```

**does not erase its contents.**

## Important options

### `-a` — Change access time only

```bash
touch -a file.txt
```

### `-m` — Change modification time only

```bash
touch -m file.txt
```

### `-c` — Don't create a missing file

```bash
touch -c file.txt
```

### `-t` — Set a specific timestamp

```bash
touch -t 202610021500 file.txt
```

## Interview question

**What happens when `touch existing.txt` is executed?**

The file contents remain unchanged, but its timestamps are updated.

---

# 6. `cp` — Copy

## Purpose

Copies files and directories.

### Syntax

```bash
cp [OPTIONS] SOURCE DESTINATION
```

### Copy a file

```bash
cp file.txt backup.txt
```

### Copy into a directory

```bash
cp file.txt backup/
```

### Copy multiple files

```bash
cp a.txt b.txt backup/
```

## Important options

### `-r` / `-R` — Recursive

Used to copy directories and their contents.

```bash
cp -r project project_backup
```

### `-i` — Interactive

Asks before overwriting an existing destination.

```bash
cp -i file.txt backup.txt
```

### `-v` — Verbose

```bash
cp -v file.txt backup.txt
```

Shows what is being copied.

### `-p` — Preserve attributes

```bash
cp -p file.txt backup.txt
```

Attempts to preserve metadata such as:

- permissions
- ownership
- timestamps

### `-a` — Archive

```bash
cp -a source destination
```

Useful for backups. It recursively copies while preserving file attributes.

## Interview question

**Why use `cp -r` for directories?**

A directory can contain nested files and directories, so its contents must be copied recursively.

---

# 7. `mv` — Move / Rename

## Purpose

Moves or renames files and directories.

### Syntax

```bash
mv [OPTIONS] SOURCE DESTINATION
```

### Move

```bash
mv file.txt documents/
```

### Rename

```bash
mv old.txt new.txt
```

### Move multiple files

```bash
mv a.txt b.txt documents/
```

## Important options

### `-i` — Interactive

Ask before overwriting.

```bash
mv -i file.txt existing.txt
```

### `-f` — Force

Do not prompt before overwriting.

```bash
mv -f file.txt destination/
```

### `-n` — No overwrite

Don't overwrite an existing destination.

```bash
mv -n file.txt destination/
```

### `-v` — Verbose

```bash
mv -v file.txt destination/
```

## Important systems concept

Moving a file **within the same filesystem** can often be very fast because Linux can change directory metadata instead of copying the file's entire contents.

Moving between different filesystems may require:

```text
copy data
   ↓
delete original
```

## Interview question

**Is `mv` always physically copying file data?**

No. Within the same filesystem, it can often update directory entries/metadata instead.

---

# 8. `rm` — Remove

## Purpose

Deletes files and directories.

### Syntax

```bash
rm [OPTIONS] FILE
```

### Delete a file

```bash
rm file.txt
```

## Important options

### `-i` — Interactive

Ask before deleting.

```bash
rm -i file.txt
```

Safer for manual use.

### `-f` — Force

```bash
rm -f file.txt
```

Does not prompt and ignores nonexistent files.

### `-r` — Recursive

```bash
rm -r project/
```

Deletes a directory and its contents recursively.

### `-rf` — Recursive + Force

```bash
rm -rf project/
```

Meaning:

```text
-r → recursive
-f → force
```

## ⚠️ Important warning

Be extremely careful with:

```bash
rm -rf
```

Linux generally does not provide a recycle bin for this command.

Never blindly execute destructive commands involving `/` or important system directories.

## Interview question

**Difference between these?**

```text
rm file
    → delete a file

rm -r directory
    → recursively delete a directory

rm -rf directory
    → recursively + force delete
```

---

# 9. `cat` — Concatenate

## Purpose

`cat` stands for **concatenate**.

It can:

1. Display file contents
2. Concatenate multiple files
3. Work with input/output redirection

### Syntax

```bash
cat [OPTIONS] [FILE]
```

### Display a file

```bash
cat file.txt
```

### Display multiple files

```bash
cat file1.txt file2.txt
```

Their contents are printed one after another.

## Important options

### `-n` — Number all lines

```bash
cat -n file.txt
```

### `-b` — Number non-empty lines

```bash
cat -b file.txt
```

### `-A` — Show non-printing characters

```bash
cat -A file.txt
```

Useful for detecting:

- tabs
- trailing spaces
- unusual characters

## Concatenation

```bash
cat file1.txt file2.txt > combined.txt
```

The `>` redirects output into a file.

### `>` — Overwrite

```bash
echo "hello" > file.txt
```

Creates or overwrites `file.txt`.

### `>>` — Append

```bash
echo "world" >> file.txt
```

Adds to the end without overwriting existing content.

Redirection will be studied in depth later.

## Important practical point

Avoid:

```bash
cat huge.log
```

for very large files because it prints everything.

Later learn:

```bash
less
head
tail
```

for efficient log inspection.

## Interview question

**What does `cat` stand for?**

Concatenate.

It is not fundamentally a "file viewer."

---

# 10. `find` — Search the Filesystem

## Purpose

Searches for files and directories based on conditions.

This is extremely useful for Cloud/DevOps troubleshooting.

### Syntax

```bash
find [PATH] [OPTIONS] [EXPRESSION]
```

---

## Find by name

```bash
find . -name "file.txt"
```

Searches from the current directory recursively.

## Find `.txt` files

```bash
find . -name "*.txt"
```

## Case-insensitive name

```bash
find . -iname "*.TXT"
```

`-iname` ignores case.

## Find files only

```bash
find . -type f
```

`f` = regular file.

## Find directories only

```bash
find . -type d
```

`d` = directory.

## Find by size

Files larger than 100 MB:

```bash
find . -type f -size +100M
```

Files larger than 1 GB:

```bash
find . -type f -size +1G
```

## Find by modification time

Modified within the last day:

```bash
find . -mtime -1
```

Modified more than 7 days ago:

```bash
find . -mtime +7
```

`mtime` works in 24-hour periods.

## Find empty files

```bash
find . -type f -empty
```

## Find and execute a command

```bash
find . -name "*.log" -exec ls -l {} \;
```

Meaning:

```text
find .
   ↓
find .log files
   ↓
run "ls -l" on each result
```

`{}` represents the file found by `find`.

`\;` terminates the `-exec` command.

## Find by permissions

```bash
find . -type f -perm 777
```

Permissions will be covered separately.

---

## Interview scenarios

### Scenario 1

> Your server is running out of disk space. Find files larger than 1 GB.

```bash
find / -type f -size +1G
```

If permission errors occur:

```bash
sudo find / -type f -size +1G
```

### Scenario 2

> Find all `.log` files under `/var/log`.

```bash
find /var/log -type f -name "*.log"
```

---

# 📌 Complete Cheat Sheet

| Command | Important options | Purpose |
|---|---|---|
| `pwd` | `-L`, `-P` | Show current directory |
| `ls` | `-l`, `-a`, `-h`, `-R`, `-t`, `-S` | List contents |
| `cd` | `..`, `~`, `-` | Navigate |
| `mkdir` | `-p`, `-v`, `-m` | Create directories |
| `touch` | `-a`, `-m`, `-c`, `-t` | Create/update timestamps |
| `cp` | `-r`, `-i`, `-p`, `-a`, `-v` | Copy |
| `mv` | `-i`, `-f`, `-n`, `-v` | Move/rename |
| `rm` | `-r`, `-f`, `-i` | Delete |
| `cat` | `-n`, `-b`, `-A` | Read/concatenate |
| `find` | `-name`, `-iname`, `-type`, `-size`, `-mtime`, `-empty`, `-exec` | Search |

---

# 🎯 What to Memorize Today

## Tier 1 — MUST KNOW

```bash
pwd
ls
ls -la
cd
cd ..
cd ~
mkdir
mkdir -p
touch
cp
cp -r
mv
rm
rm -r
cat
find
find . -name "*.txt"
find . -type f
```

## Tier 2 — Understand

```bash
pwd -L
pwd -P
ls -lh
ls -lt
ls -lS
cp -a
cp -p
mv -i
rm -i
cat -n
find -type d
find -size
find -mtime
find -exec
```

---

# 🧠 Linux Interview Mental Model

When given a basic Linux problem:

```text
Where am I?
    ↓
pwd

What's here?
    ↓
ls

Where do I need to go?
    ↓
cd

Do I need to create something?
    ↓
mkdir / touch

Do I need to copy something?
    ↓
cp

Do I need to move/rename something?
    ↓
mv

Do I need to delete something?
    ↓
rm

Do I need to inspect a file?
    ↓
cat

Do I need to locate something?
    ↓
find
```

---

# 🔍 Don't Memorize Every Flag

A strong Linux engineer does **not** memorize every option of every command.

Know the common ones, and know how to discover the rest:

```bash
man ls
man find
man cp
```

or:

```bash
ls --help
find --help
```

The ability to read documentation is itself an important Linux skill.

---

# 🧪 Practice Task

Create this structure using only the commands learned today:

```text
linux-practice/
├── projects/
│   ├── python/
│   └── cloud/
├── notes/
│   ├── linux.txt
│   └── commands.txt
└── backup/
```

Then:

1. Create `python/app.py`
2. Create `cloud/aws.txt`
3. Copy `app.py` into `backup`
4. Rename `aws.txt` → `aws-notes.txt`
5. Find all `.txt` files
6. Delete the `backup` directory
7. Explain the difference between:

```text
.
..
~
/
```

---

## Next Topic

After mastering these 10, move to:

```text
grep
  ↓
head / tail
  ↓
less
  ↓
wc
  ↓
sort
  ↓
uniq
  ↓
cut
  ↓
awk
  ↓
sed
```

These commands are particularly important for **log analysis, shell scripting, automation, and Cloud/DevOps interviews**.
